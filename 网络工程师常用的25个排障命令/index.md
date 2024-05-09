# 网络工程师常用的25个排障命令




在网络运维工作中，掌握排障命令可以帮助我们快速定位和解决各种网络故障，确保网络稳定运行。

今天要和大家分享的是关于**网络排障中常用的25个命令**。



##### **1、Ping测试**

**方法：**使用Ping命令测试目标设备的连通性。

**命令：**在命令行界面中输入以下命令

ping 目标设备的IP地址或域名

示例: （假设目标IP地址为10.0.0.1）

<设备> ping 10.0.0.1



**
**

##### **2、Traceroute/Tracepath**

方法：使用tracert命令（Windows）或traceroute命令（Linux）查看数据包的路由路径

命令：在命令行界面中输入以下命令

tracert 目标设备的IP地址或域名 



示例: （假设目标IP地址为10.0.0.1）


<设备> tracert 10.0.0.1

**
**

##### **3、Telnet/SSH远程登录**

方法：使用Telnet或SSH协议远程连接到目标设备，以查看和管理设备

命令（SSH）：在命令行界面输入以下命令

ssh 用户名@目标设备的IP地址或域名



示例: （假设用户名为admin，目标IP地址为10.0.0.1）

<设备> ssh admin@10.0.0.1

**
**

##### **4、路由表和ARP表检查**

方法：查看路由器上的路由表和ARP表

命令（路由表）：在命令行界面中输入以下命令



display ip routing-table 



<设备>display ip routing-table 


命令（ARP表）：在命令行界面中输入以下命令

display arp

<设备>display arp


**
**

##### **5、日志分析**

**
**方法：查看设备和服务器上的日志文件，以查找与网络问题相关的错误或异常信息

示例：使用命令查看设备上的日志文件

<设备> display logbuffer

**
**

##### **6、端口和服务检查**

方法：确认设备的端口和服务配置是否正确 ，包括防火墙规则和ACL

示例：查看设备的端口配置和防火墙规则

<设备>

display current-configuration | include port-group

<设备>display firewall configuration

##### **7、更新和备份

**
方法：定期更新设备固件和备份配置，以防止故障和数据丢失。

示例：执行备份和更新操作

<设备> save
<设备>upgrade software filename.bin

**
**

##### **8、DNS查询**

方法：使用ping 命令测试DNS解析是否正确

示例：使用ping测试域名解析

<设备>ping www.example.com

**
**

##### **9、防火墙规则检查

**
方法：查看防火墙规则配置，确保允许必要的流量通过



示例：查看防火墙规则

<设备> display firewall zone

<设备>display firewall rule

**
**

##### **10、VLAN配置检查**

方法：查看交换机上的VLAN配置，确保设备位于正确的VLAN中

示例：查看VLAN配置

<设备>display vlan

**
**

##### **11、MTU大小检查**

方法：检查网络设备的最大传输单元（MTU）设置，确保它们匹配

示例：查看接口MTU配置



<设备>

display interface GigabitEthernet0/0/1

**
**

##### **12、负载均衡配置检查**



方法：查看负载均衡设备的配置，确保流量均匀分配

示例：查看服务器农场配置

<设备>display server-farm

**
**



##### **13、BGP邻居状态检查**



方法：检查BGP邻居状态，确保BGP路由正常传播

示例：查看BGP邻居状态

<设备>display bgp peer



##### **14、子网掩码检查**



方法：检查子网掩码是否正确配置，以确保IP地址分配正确

示例：查看接口配置

<设备>

display ip interface GigabitEthernet0/0/1

**
**

**
**

##### 15、MTU Path Discovery

方法：使用MTU Path Discovery检查网络路径的最大传输单元

示例：启用 MTU Path Discovery

<设备>system-view



<设备>ip mtu discovery


**
**

##### **16、ACL规则检查**

方法：检查访问控制列表(ACL)规则，确保允许或阻止了正确的流量

示例：查看ACL规则

<设备>display acl 2000

**
**

##### **17、DHCP规则检查**

方法：检查DHCP服务器分配的IP地址，确保正确配置

示例：查看DHCP分配信息

<设备> display dhcp server ip-in-use


**
**

##### **18、链路聚合检查**

方法：检查链路聚合组（LAG）配置，确保链路均衡正常。

示例：查看LAG配置

<设备>display link-aggregation verbose

**
**

##### **19、MAC地址表检查**

方法：查看交换机MAC地址表，确保MAC地址分发正确。

示例：查看MAC地址表

<设备>display mac-address

**
**

##### **20、系统资源利用率监控**

方法：监控CPU、内存和存储等系统资源的利用率

示例：查看系统资源利用率

<设备>display resource usage

**
**

##### **21、ACL日志分析**

方法：查看ACL规则匹配日志，以检查是否有流量被ACL阻止

示例：查看ACL日志

<设备>display acl log

**
**

##### **22、链路状态检查**

方法：检查链路状态，确保链路是否正常连接

示例：查看链路状态

<设备>display interface brief

**
**

##### **23、DNS服务器可用性检查**

方法：使用nslookup命令检查DNS服务器的可用性

示例：测试DNS服务器可用性

<设备>ping dns-server-ip

**
**

##### **24、OSPF邻居状态检查**

方法：检查OSPF邻居状态，确保路由协议正常工作。

示例：查看OSPF邻居状态

<设备> display ospf peer

**
**

##### **25、冗余路由和HA状态检查**

方法：检查冗余路由和高可用性(HA)配置，确保备用设备正常工作

示例：查看HA状态

<设备>display standby





对于工作中遇到的网络故障，不仅仅是记住这些命令，重点是能够熟练的运用这些命令使用排除法来找到最终的网络故障原因。

