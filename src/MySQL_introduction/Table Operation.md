2019年10月11日10:20:49
## 表的操作

提示：  
[ ] 代表选填，里的汉字是注释。   
| 表示 或者   
sql语句默认不区分大小写，由COLLATE属性决定。

### 创建表
**`create [temporary] table [库名.] 表名 （表结构定义）[表选项]`** 
###### *temporary 临时表，会话结束表自动消失*   
###### 表结构定义：  
`字段名 数据类型 [not null|null] [DEFAULT default_value] [AUTO_INCREMENT]`  
每个字段必须有数据类型  
每个字段逗号间隔，最后一个字段后不能有逗号  
###### 表选项   
1. 字符集  
`CHARSET = charset_name` 默认数据库字符集。*
2. 存储引擎  
`ENGINE = engine_name`  
>表在管理数据时采用的不同的数据结构，结构不同会导致处理方式、提供的特性操作等不同  
>常见的引擎：InnoDB MyISAM Memory/Heap BDB Merge Example CSV MaxDB Archive  
>不同的引擎在保存表的结构和数据时采用不同的方式  
>MyISAM表文件含义：.frm表定义，.MYD表数据，.MYI表索引  
>InnoDB表文件含义：.frm表定义，表空间数据和日志文件  

* `SHOW ENGINES `-- 显示存储引擎的状态信息  
* `SHOW ENGINE 引擎名 LOGS|STATUS` -- 显示存储引擎的日志或状态信息

3. 数据文件目录
        `DATA DIRECTORY = '目录'`
4. 索引文件目录
        `INDEX DIRECTORY = '目录'`
5. 表注释
        `COMMENT = 'string'`

### 查看表（非内容）    
#### 列出所有表        
`show tables;`  
`show tables from *库名*`
#### 查看表结构
展示表结构  
`DESC 表名 `  
`DESCRIBE 表名 `  
`EXPLAIN 表名`   
`SHOW COLUMNS FROM 表名 `  
展示建表语句   
`show create table *表名*`  
展示数据库中的所有表信息（表选项的内容）。  
`show table status [from db_name]`

### 修改表
#### 修改表选项
`alter table 表名 表选项 `  
ex: `alter table *表名* engine=MyISAM;`
#### 表重命名
`rename table 原表名 to 新表名`  
`rename table 原表名 to 库名.表名` 可以利用重命名将表移动到另一个数据库。

#### 修改**表字段**结构
`alter table 表名 操作`
###### 操作：
1. add
   1. *添加字段，first表示增加在第一个 默认是从后面加*  
   `add 字段名 { after 字段名 | first } `   
   2. 创建主键  
   `add primary key(字段名）`  
   3. 创建唯一索引  
   `add unique [索引名] (字段名)`
   4. 创建普通索引  
   `add index [索引名] (字段名)`

2. drop
   1. 删除字段  
   `drop 字段名`
   2. 对某字段属性进行修改，不能修改字段名  
  ` modify 字段名 字段属性`
   3. 支持对字段名进行修改了  
   `change 原字段名，新字段名，字段属性。`
   4. 删除主键（删除主键前需要删除其AUTO_INCREMENT属性）  
   `drop primary key `
   5. 删除索引  
   `drop index 索引名`
   6. 删除外键  
   ` drop foreign key `
   
   
3. 删除表  
`drop table 表名`
4. 清空表数据  
`truncate [table] 表名`
5. 复制表结构  
`create table 表名 like 要复制的表名`
6. 复制表结构和数据  
`create table 表名 select & from 要复制的表名`
7. 检查是否有错误  
`check table 表名 [, 表名] ...[option]`
8. 优化表  
` optimize [local|no_write_to_binlog] table 表名 [,表名]...`
9. 修复表  
`repair [LOCAL | NO_WRITE_TO_BINLOG] TABLE tbl_name [, tbl_name] ... [QUICK] [EXTENDED] [USE_FRM]`
10. 分析表  
`analyze [local|no_write_to_binlog] table 表名 [,表名]...`

