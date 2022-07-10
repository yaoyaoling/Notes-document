## Consul

## Consul **base commond** 

| Type | Command           | Remark |
| ---- | ----------------- | ------ |
| 启动 | consul agent -dev |        |
| 查看 | localhost:8500    |        |

 

## Windows - CMD命令

| Type     | Command                                      | Remark |
| -------- | -------------------------------------------- | ------ |
| 进入目录 | cd  E:\03.Consul\consul_1.11.5_windows_amd64 |        |
| 启动     | consul agent -dev                            |        |
| 查看     | #浏览器打开<br />localhost:8500              |        |

 

## Linux - CMD命令

下载地址

1. https://www.github.com/hashicorp/consul
2. https://www.consul.io/downloads 



- 解压版

  ```shell
  # 下载地址
  https://releases.hashicorp.com/consul/1.11.5/consul_1.11.5_linux_arm64.zip
  
  # 1. 解压： 
  unzip consul_1.10.1_linux_amd64.zip
  
  # 2. 配置环境变量： 
  vim /etc/profile
  #添加一下配置：
  CONSUL_HOME=/usr/local/consul/consul
  export   PATH=$PATH:CONSUL_HOME
  	
  # 3. 刷新环境变量： 
  source /etc/profile
  
  # 4.验证是否安装成功：
  ./consul -v
  
  # 5. 启动agent（默认8500）：
  nohup ./consul agent -dev -client 0.0.0.0 -ui &
  
  # 6. 验证8500端口是否启动：
  netstat -anp|grep 8500
  
  # 7. 浏览器访问： http://192.168.60.128:8500/ （CentOS的ip）    
  ```



| id   | Type                 | Content                                                      | Remark                                                       |
| ---- | -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1    | 解压版               | https://releases.hashicorp.com/consul/1.11.5/consul_1.11.5_linux_arm64.zip       <br />1. 解压： unzip consul_1.10.1_linux_amd64.zip    <br />2. 配置环境变量： vim /etc/profile，添加一下配置：      <br />CONSUL_HOME=/usr/local/consul/consul      <br />export   PATH=$PATH:CONSUL_HOME       <br />3. 刷新环境变量： source /etc/profile    <br />4.验证是否安装成功：./consul -v    <br />5. 启动：<br />* 启动agent（默认8500）：nohup ./consul agent -dev -client 0.0.0.0 -ui &     <br />* 验证8500端口是否启动：netstat -anp\|grep 8500     <br />* 浏览器访问： http://192.168.60.128:8500/ （CentOS的ip） |                                                              |
| 2    | 安装版               | sudo yum install -y  yum-utils<br />sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo  sudo yum -y install  consul<br />#安装路径<br />whereis consul |                                                              |
| 3    | 启动consul  (client) | consul agent -dev<br />consul agent -dev -ui  -node=consul-dev -client=192.168.100.158<br />consul agent -dev -ui  -node=consul-dev -client=0.0.0.0<br />consul agent -dev -ui  -client=0.0.0.0 | -dev标志来快速设置一个开发服务器  <br />-client 为服务器端IP |
| 4    | 启动consul  (server) | consul  agent -server -ui -bootstrap-expect=3 -data-dir=/tmp/consul -node=consul-node1 -client=0.0.0.0 -bind=127.0.0.1  -datacenter=dc1<br />consul agent -server -ui -bootstrap-expect=3 -data-dir=/tmp/consul  -node=consul-node2 -client=0.0.0.0 -bind=127.0.0.1 -datacenter=dc1<br />consul agent -server -ui -bootstrap-expect=3 -data-dir=/tmp/consul  -node=consul-node3 -client=0.0.0.0 -bind=127.0.0.1 -datacenter=dc1 |                                                              |
| 5    | 查看节点成员         | consul members  <br />consul  members -detailed              |                                                              |
| 6    | 查看                 | #浏览器打开  <br />localhost:8500                            |                                                              |