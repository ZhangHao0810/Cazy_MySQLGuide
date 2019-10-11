2019年10月11日08:18:28
## 连接数据库

#### 1.直接用数据库编辑器连接和打开。


#### 2.从MySQL Command Line Client 进行操作：

直接打开 显示：  
`Enter password: `  
输入密码即可连接数据库。 


#### 3.从CMD进行操作：

1. 从CMD启动Mysql  
  ` net start mysql  `
   
 2. 从CMD连接/断开服务器（先进入mysql.exe 的路径。）：  
`mysql  -h 主机号  -p端口号  -u 用户名 -p 密码`  
    * 本地的话，主机号和端口号可以省略  
ex:   
`cd C:\Program Files\MySQL\MySQL Server 5.5\bin`    
`C:\Program Files\MySQL\MySQL Server 5.5\bin>mysql.exe -u root -p`    
`Enter password: `  
`....... `  
之后就跟在 MySQL Command Line Client 客户端的操作一致了。



show processlist  ----显示那些线程在运行   
show variables  ----- 显示变量