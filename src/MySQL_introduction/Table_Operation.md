2019年10月11日10:20:49
## 表的操作

提示：  
[ ] 代表选填，里的汉字是注释。   
| 表示 或者   
sql语句默认不区分大小写，由COLLATE属性决定。

### 1.创建表
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

### 2.查看表（非内容）    
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

### 3.修改表
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
   
   
###  4.删除表  
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



2019年10月13日10:01:13 
## select语句

`select [all|distinct] select_expr from -> where -> group by [合计函数] -> having -> order by -> limit`

#### distinct, all 选项 
distinct 去除重复记录    
默认为 all, 全部记录

#### select_expr 
  -  可以用 * 表示所有字段。  
  `select * from tb;`
  -  可以使用表达式（计算公式、函数调用、字段也是个表达式）   
  `select stu,29+25, now() from tb;`
-    可以为每个列使用别名。查询结果以别名显示。用于简化列标识，避免多个列标识符重复。
        - 使用 as 关键字，也可省略 as.  
         `select stu+10 as add10 from tb;`

####  from 子句
   - 用于标识查询来源。
-    可以为表起别名。查询结果以别名显示。使用as关键字。  
     `select * from tb1 as tt, tb2 as bb;`
   - from子句后，可以同时出现多个表。
     - 多个表会横向叠加到一起，而数据会形成一个 [笛卡尔积](笛卡尔积.jpg) 。  
       ` select * from tb1, tb2;`

#### where 子句
  - 从from获得的数据源中进行筛选。
  - 整型1表示真，0表示假。 
    -   运算符：    
        =, <=>, <>, !=, <=, <, >=, >, !, &&, ||,   
        in (not) null, (not) like, (not) in, (not) between and,
        is(not),and, or, not,  is/is not  
        加上ture/false/unknown，检验某个值的真假      
- 关系运算符:  > >= < <= !=  <>
    - 判断某一列是否为空: is null is not null  
​		in 在某范围内  
​		between...and  
- 逻辑运算符: and or not
- 模糊查询:  like    
    - _ : 代表单个字符  
    - %: 代表的是多个字符  
        
        

#### group by 子句, 分组子句  
  `group by 字段/别名 [排序方式]`  
  [排序方式]。升序：`ASC`，降序：`DESC` 分组之后会进行排序。·
   
 - 以下[合计函数]需配合 group by 使用：
    - count 返回不同的非NULL值数目 `count(*)、count(字段)`  
    - sum 求和  
    - max 求最大值  
    - min 求最小值  
    - avg 求平均值  
    - group_concat  
       返回带有来自一个组的连接的非NULL值的字符串结果。组内字符串连接。       

例：   
` mysql> select name,sum(score < 60),avg(score) as pj from
       stu group by name; `
#### having 子句，条件子句 
- 相当于where，只是执行时机不同。
- SQL标准要求HAVING必须引用GROUP BY子句中的列或用于合计函数中的列。
- where 在开始时执行检测数据，对原数据进行过滤。 
- having对筛选出的结果再次进行过滤。
-  having 字段必须是查询出来的，where字段必须是数据表存在的。 
-  where 不可以使用字段的别名，having可以。
-  因为执行WHERE代码时，可能尚未确定列值。
-   where不可以使用合计函数。一般需用合计函数才会用 having

例子：   
`mysql> select name,sum(score < 60) as gk ,avg(score) as pj from
stu group by name having gk >=2; `

#### order by  
` order by 排序字段/别名 排序方式[,排序字段/别名 排序方式]... `  
升序：ASC，降序：DESC 
支持多个字段的排序。

#### limit 子句，限制结果数量子句
仅对处理好的结果进行数量限制。将处理好的结果的看作是一个集合，按照记录出现的顺序，索引从0开始。    
`limit 起始位置, 获取条数 `  
省略第一个参数，表示从索引0开始。limit 获取条数


#### UNION  将多个select查询的结果组合成一个结果集合。
`SELECT ... UNION [ALL|DISTINCT] SELECT ...`  

默认 DISTINCT 方式，即所有返回的行都是唯一的  
建议，对每个SELECT查询加上小括号包裹。  
ORDER BY 排序时，需加上 LIMIT 进行结合。  
需要各select查询的字段数量一样。  
每个select查询的字段列表(数量、类型)应一致，因为结果中的字段名以第一条select语句为准。  