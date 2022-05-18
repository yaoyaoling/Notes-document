# 0.Base Command

|      | 描述     | Command                 |
| ---- | -------- | ----------------------- |
| 1    | 发行版本 | cat /etc/redhat-release |

 

# 1.网络 & 防火墙 & 进程

**网络 & 进程**

|      | 描述                   | Command                                                      |
| ---- | ---------------------- | ------------------------------------------------------------ |
| 1    | 查看IP地址             | ip addr  <br />ifconfig  <br />#[yum](https://so.csdn.net/so/search?q=yum&spm=1001.2101.3001.7020) install  net-tools -y |
| 2    | 设置静态IP             | /etc/sysconfig/network-scripts/ifcfg-<NIC Name>  <br />TYPE="Ethernet"  PROXY_METHOD="none"  <br />BROWSER_ONLY="no"  <br />**BOOTPROTO="static"     # 使用静态IP地址，默认为<br />dhcp**  **IPADDR="192.168.8.119"   # 设置的静态IP地址**  <br />**NETMASK="255.255.255.0"  # 子网掩码**  <br />**GATEWAY="192.168.8.1"   # 网关地址**  <br />**DNS1="114.114.114.114"   # DNS服务器**  <br />DEFROUTE="yes"  IPV4_FAILURE_FATAL="no"  <br />IPV6INIT="yes"  IPV6_AUTOCONF="yes"  <br />IPV6_DEFROUTE="yes"  <br />IPV6_FAILURE_FATAL="no"  <br />IPV6_ADDR_GEN_MODE="stable-privacy"  <br />NAME="ens33"  <br />UUID="95b614cd-79b0-4755-b08d-99f1cca7271b"  <br />DEVICE="ens33"  <br />ONBOOT="yes"       #是否开机启用 |
| 2    | 重启网卡               | service  network restart                                     |
| 3    | 测试网络               | nslookup [www.baidu.com](http://www.baidu.com)               |
| 4    | 查看端口使用情况       | netstat  -tunlp  netstat  -lnpt                              |
|      | 检查端口被哪个进程占用 | netstat  -lnpt \|grep <port>                                 |
|      | 查看进程的详细信息     | ps  <process id>                                             |

**防火墙**

|      | 描述                              | Command                                                      |
| ---- | --------------------------------- | ------------------------------------------------------------ |
| 1    | Base command  (firewalld)         | #防火墙状态  <br />systemctl  status firewalld  <br />#开启 / 关闭 / 重启 防火墙  <br />systemctl start  firewalld  <br />systemctl  stop firewalld <br />systemctl  restart firewalld  <br />#设置防火墙开机  <br />systemctl  disable firewalld  <br />systemctl  enable firewalld  <br />*#重新加载防火墙配置才会起作用*  <br />firewall-cmd --reload |
| 2    | 查看配置(firewalld)               | firewall-cmd --state   firewall-cmd  --list-all              |
|      | 查看开放端口(firewalld)           | firewall-cmd  --zone=public --list-ports  firewall-cmd  --list-ports |
| 3    | 开放端口(firewalld)               | firewall-cmd  --permanent --add-port=80/tcp                  |
| 4    | 移除规则(firewalld)               | firewall-cmd  --permanent --remove-port=80/tcp               |
| 5    | 放通端口段(firewalld)             | firewall-cmd  --permanent --zone=public --add-port=1000-2000/tcp |
| 6    | 放通IP访问，默认允许(firewalld)   | firewall-cmd  --permanent --add-rich-rule='rule family=ipv4 source address=192.168.1.169  accept' |
|      |                                   |                                                              |
| 1    | Base command  (iptables-services) | #安装  <br />yum installl  iptables-services  <br />#防火墙状态  <br />service  iptables status  <br />#开启 / 关闭 / 重启 防火墙  <br />service iptables start  <br />service  iptables stop  <br />service iptables restart  <br />#永久开启 / 关闭防火墙  chkconfig  iptables on  chkconfig  iptables off |

 

**问题**

|      | 描述                                                         | Command                                                      |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1    | 当执行 ifup ens33  <br />出现错误：<br />Error:Connection activation failed: No suitable device  found for this connection | chkconfig NetworkManager off  <br />chkconfig network on  <br />service NetworkManager stop  <br />service network start |
| 2    | 端口无法访问                                                 | 查看防火墙开放端口信息：service iptables status  <br />防火墙开放对应端口  <br />/sbin/iptables -I INPUT -p tcp --dport 7071 -j  ACCEPT #开启7071端口  <br />/etc/rc.d/init.d/iptables save #保存配置  <br />/etc/rc.d/init.d/iptables restart #重启服务 |
| 3    | ssh连接慢解决方法                                            | **调整/etc/ssh/sshd_config**     <br />su root (以root用户登录)   <br />vi /etc/ssh/sshd_config   <br />输入 / ,查找GSSAPIAuthentication 赋值为no   <br />输入 / ,查找UseDNS,赋值为 no(放开该项，去掉#)   <br />!wq保存文件    <br />**重启sshd**     <br />systemctl       restart sshd |

 

# 2.安装图形界面

**Command**

|      | 描述         | Command |
| ---- | ------------ | ------- |
| 1    | 进入图像界面 | startx  |

 

**安装图形界面**

|      | 描述                                   | Command                             |
| ---- | -------------------------------------- | ----------------------------------- |
| 1    | 安装X(X Window System)                 | yum  groupinstall "X Window System" |
| 2    | 安装图形界面软件，GNOME(GNOME Desktop) | yum  groupinstall "GNOME Desktop"   |

 

# 3.yum

|      | 描述          | Command                                                      |                                                              |
| ---- | ------------- | ------------------------------------------------------------ | :----------------------------------------------------------- |
| 1    | 更新yum       | yum update                                                   |                                                              |
| 2    | 查看yum最快源 | yum  makecache fast                                          |                                                              |
| 3    | 清空缓存      | yum clean all                                                |                                                              |
| 4    | 生成缓存      | yum mackecache                                               |                                                              |
| 3    | 设置仓库      | #安装yum-utils <br />yum  install -y yum-utils device-mapper-persistent-data lvm2<br /><br />#设置稳定的仓库  <br />yum-config-manager --add-repo http://xxxx<br />yum-config-manager  --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo | 安装所需的软件包。yum-utils  提供了 yum-config-manager ，并且 device mapper 存储驱动程序需要  device-mapper-persistent-data 和 lvm2. |
| 5    | 查看版本List  | yum list docker-ce --showduplicates \| sort -r               |                                                              |
| 6    | 安装          | #安装默认稳定版本<br />yum -y  install docker-ce<br />#安装指定版本 其中<VERSION_STRING>为版本号<br />sudo yum  install docker-ce-<VERSION_STRING> |                                                              |
| 7    | 卸载          | **yum remove** docker \ <br />docker-client \ <br />docker-client-latest  \ <br />docker-common \ <br />docker-latest \ <br />docker-latest-logrotate \ <br />docker-logrotate \ <br />docker-engine | #删除安装包<br />yum  remove docker-ce<br />#删除镜像、容器、配置文件等内容<br />rm -rf  /var/lib/docker |

 

**问题**

|      |                                                              |                                                              |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1    | 出现错误：<br />http://mirrors.163.com/centos/5/os/i386/repodata/repomd.xml:  <br />[Errno 14] HTTP Error 404: Not Found Trying  other mirror.  <br />原因：yum源失效 | 更新yum源：  <br />yum clean all  <br />yum makecache  <br />yum update |
|      |                                                              |                                                              |