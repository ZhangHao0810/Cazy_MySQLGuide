2019年10月11日18:53:21


提示：  
[ ] 代表选填，里的汉字是注释。   
| 表示 或者   
sql语句默认不区分大小写，由COLLATE属性决定。

## 数据的操作
#### 增
`INSERT [INTO] 表名 [(字段列表)] VALUES (值列表) [, (值列表), ...]`  
- 如果要插入的值列表包含所有字段并且顺序一致，则可以省略字段列表。  
- 可同时插入多条数据记录！  
- `REPLACE` 与 `INSERT` 完全一样，可互换。     
`    INSERT [INTO] 表名 SET 字段名=值[, 字段名=值, ...]` 
#### 查
`    SELECT 字段列表 FROM 表名[ 其他子句]`
- 可来自多个表的多个字段
- 其他子句可以不使用
- 字段列表可以用*代替，表示所有字段
#### 删
` DELETE FROM 表名[ Where条件子句]`
- 没有条件子句，则会删除全部
#### 改
` UPDATE 表名 SET 字段名=新值[, 字段名=新值] [Where条件]`