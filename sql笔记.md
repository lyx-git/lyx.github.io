# sql优化  

  - in 和 exists 的选择
    - in 适用于子查询的表比原表要小的时候
    - exists 适用于子查询的表比原表要大的时候
    
  - not in 和 not exists 的选择
    - not exists 比 not in 的效率要高
    
  - or 和 union 的选择
    - or 一般不要选择使用or这种方式
    - union 一般在遇到使用or的时候，可以采取使用union，因为使用or就要求or前后使用的列，都必须要有索引，才会使用索引，而使用union进行结果集合并，就不会有这种情况
    
  - union 和 unionAll 的选择
    - union 表示用于合并两个或多个select语句的结果集，并且去除重复数据，按照数据库字段的顺序进行排序
    - unionAll 用于合并两个或多个select语句的结果集，不去重复数据，不排序
  
  - 数据库表复制（同一个服务器，数据库表的复制）
    - insert into 数据库名称.目标表名称 select * from 数据库名称.源表名称
    
  - 不同服务器之间，数据库表的的复制，使用navicat工具比较方便
