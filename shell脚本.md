#!/bin/bash
# export表示设置环境变量，作用在整个shell脚本中 
# export JAVA_HOME=/opt/websoft/jdk/jdk1.8.0_231
# export JRE_HOME=/$JAVA_HOME/jre
# export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
# export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin

#这里可替换为你自己的执行程序，其他代码无需更改
# 基础jvm设置
JAVA_OPTS="-server  -Xms20G   -Xmx20G  -Xmn8G  -XX:MetaspaceSize=512M -XX:MaxMetaspaceSize=512M -XX:SurvivorRatio=4"
#GC设置
JAVA_OPTS="$JAVA_OPTS -verbose:gc -Xloggc:$LOG_HOME/gc.log -Djava.awt.headless=true -XX:+PrintGCDateStamps -XX:+PrintGCDetails  -Dsun.rmi.dgc.server.gcInterval=600000 -Dsun.rmi.dgc.client.gcInterval=600000 -XX:+UseG1GC -XX:MaxGCPauseMillis=1000 -XX:+PrintHeapAtGC"
#jvm监控设置
JAVA_OPTS="$JAVA_OPTS -Djava.rmi.server.hostname=10.1.85.36 -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=65535 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false"

APP_NAME=/opt/websofts/spring-applications/apps/bigdata/BigDataFile.jar

#使用说明，用来提示输入参数
usage() {
  echo "Usage: sh startbigdata.sh [start|stop|restart|status]"
  exit 1
}

#检查程序是否在运行
is_exist() {
  pid=`ps -ef|grep $APP_NAME | grep -v grep | awk '{print $2}'`
  #如果不存在返回1，存在返回0
  if [-z "$pid"]; then
    return 1
  else
    return 0
  fi
}

#启动方法
start() {
  is_exist
  if [$? -eq "0"]; then
    echo "${APP_NAME} is already running. pid=${pid}"
  else
    nohup java $JAVA_OPTS -jar ${APP_NAME} > bigdata-server.out 2>&1 &
  fi
}

#停止方法
stop() {
  is_exist
  if [$? -eq "0"]; then
    kill -9 ${pid}
  else
    echo "${APP_NAME} is not running"
  fi
}

#输出运行状态
status() {
  is_exist
  if [$? -eq "0"]; then
    echo "${APP_NAME} is running. pid is ${pid}"
  else
    echo "${APP_NAME} is not running."
  fi
}

#重启
restart() {
  stop
  sleep5
  start
}

#根据输入参数，选择执行对应方法，不输入则执行使用说明
case "$1" in
  "start")
    start
    ;;
  "stop")
    stop
    ;;
  "status")
    status
    ;;
  "restart")
    restart
    ;;
  *)
    usage
    ;;
esac
