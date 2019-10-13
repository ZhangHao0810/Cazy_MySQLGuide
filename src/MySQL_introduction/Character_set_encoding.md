
2019年10月11日19:00:14

### 字符集编码

- MySQL、数据库、表、字段均可设置编码
- 数据编码与客户端编码不需一致

查看所有字符集编码项：  

`SHOW VARIABLES LIKE 'character_set_%'`

    character_set_client        客户端向服务器发送数据时使用的编码
    character_set_results        服务器端将结果返回给客户端所使用的编码
    character_set_connection    连接层编码
    
`SET 变量名 = 变量值`

    set character_set_client = gbk;
    set character_set_results = gbk;
    set character_set_connection = gbk;

`SET NAMES GBK;`    -- 相当于完成以上三个设置 

### 校对集COLLATE
- 校对集用以排序  

查看所有字符集  
    `SHOW CHARACTER SET `    
    `SHOW CHARSET `  
查看所有校对集    
`    SHOW COLLATION  `  
设置字符集编码  
`    charset 字符集编码        `  
设置校对集编码  
`    collate 校对集编码        `