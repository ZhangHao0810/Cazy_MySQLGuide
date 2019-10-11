2019年10月11日09:36:56
## 数据库操作 


#### 使用库
`use *数据库名*;` 
##### 查看当前使用的数据库
`select database();`
##### 显示当前时间，用户名，数据库版本
`select now(),user(),version();`

#### 创建库
`create database *数据库名 选项信息1（设置字符集） 选项信息2（设置COLLATE）  *`  
选项信息可以不填，有默认值。看配置文件。  
*设置字符集：  
CHARACTER SET charset_name    ---表示应用的字符集  
设置COLLATE：  
COLLATE collation_name*       ---表示应用的COLLATE  
1. 有关字符集  
*建议字符集为：utf8mb4*  
    mysql中有utf8和utf8mb4两种编码，在mysql中请大家忘记**utf8**，永远使用**utf8mb4**。  
    这是mysql的一个遗留问题，mysql中的utf8最多只能支持3bytes长度的字符编码，  
    对于一些需要占据4bytes的文字，mysql的utf8就不支持了，要使用utf8mb4才行。

2. 有关COLLATE  
*utf8mb4编码的COLLATE 默认值为utf8mb4_general_ci* 
>CollATE属性决定了数据库sql语句是否区分大小写，默认值是不区分的
>COLLATE类型来告知mysql如何对字符类型的列进行排序和比较  
>COLLATE会影响到ORDER BY语句的顺序，会影响到WHERE条件中大于小于号筛选出来的结果，会影响**DISTINCT**、**GROUP BY**、**HAVING**语句的查询结果。会影响索引创建  
[具体的COLLATE知识 点此进入](https://zhuanlan.zhihu.com/p/51078373)

#### 查看已有库
`show databases;`
#### 查看当前库信息(即创建库时的字符集等信息)；
`show create databases *数据库名*;`
#### 修改库的选项信息
`alter database *库名 选项信息*`
#### 删除库
`drop database *数据库名*` 同时删除该库相关的目录及其目录内容。