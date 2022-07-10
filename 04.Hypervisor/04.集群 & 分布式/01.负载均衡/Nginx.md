# Ngnix

## ngnix.conf

| Path                             | Type       | Command                                                      |
| -------------------------------- | ---------- | ------------------------------------------------------------ |
| server -> listen                 | 监听端口   | listen    800;                                               |
| server -> server_name            | 域名       | server_name  localhost;                                      |
| server -> location               | 匹配路径   | location / ：默认返回Ngnix  index页面                        |
| server -> location -> proxy_pass | 代理转发   | proxy_pass  http://webservers;        #服务器列表  <br />#proxy_pass   http://localhost:8001/; |
| upstram                          | 服务器列表 | upstream  webservers {    <br />server localhost:8001 weight=10;    <br />server localhost:8002 weight=10;    <br />server localhost:8003 weight=10;  <br />} |
|                                  |            |                                                              |

 

## Linux

**Ngnix base commond** 

| Type         | Command                      | Remark                                                       |
| ------------ | ---------------------------- | ------------------------------------------------------------ |
| 启动         | nginx start                  |                                                              |
| 暂停         | nginx -s stop  nginx -s quit | stop - 停止服务  quit - 有链接时会等待链接请求完成时 ,在杀死worker进程 |
| 重启         | nginx -s  reload             | 重新加载配置文件ngnix.conf                                   |
| 检查         | ngnix -t                     | 检查ngnix配置是否正确                                        |
| 帮助         | ngnix -h                     |                                                              |
| 版本         | nginx -V                     |                                                              |
| 日志         | nginx -s  reopen             |                                                              |
| 指定配置文件 | ngnix -c filename            |                                                              |

 

| Content       | Command                                |
| ------------- | -------------------------------------- |
| 端口占用程序  | netstat  -ano \| findstr 80            |
| 查看nginx进程 | tasklist  /fi "IMAGENAME eq nginx.exe" |
| 杀死进程      | taskkill  /f /t /im nginx.exe          |

 

## Windows 

| Content                 | Command                               |      |
| ----------------------- | ------------------------------------- | ---- |
| 启动                    | start nginx                           |      |
| 按照指定配置去启动nginx | nginx -c  conf/nginx.conf             |      |
| 停止，kill指定进程      | nginx -s stop                         |      |
| 测试配置文件语法正确性  | nginx -t -c  conf/nginx.conf          |      |
| 版本信息                | nginx -v                              |      |
| 查看进程                | tasklist /fi "imagename eq nginx.exe" |      |

 

 