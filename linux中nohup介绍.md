# [nohup](https://blog.csdn.net/lovewebeye/article/details/82934049)介绍
  - 表示不挂断运行，让应用程序在后台运行，不会因为终端的关闭，应用程序也关闭
  - &
    - nohup通常和 & 符号一起使用
  - \>file 2>&1
    - 1 表示标准输出
    - 2 表示标准错误
    - 这句话的意思表示：标准输出重定向到file文件，标准错误重定向到标准输出
