# 黑群晖 Active Backup for Business 套件激活方法


黑群晖 Active Backup for Business 套件激活方法

首先我们先安装好Active Backup for Business套件

这时候打开会显示需要激活

我们到【控制面板】 - 【信息中心】 找到【产品序列号】并记下来



## 群晖6.X激活方法如下：

浏览器输入如下地址，显示如下信息即可进行下一步：（IP地址替换为NAS的地址，登陆用户名和登陆密码就是你登陆群晖的时候所使用的）

**群晖默认https端口为5001而不是443**

```
https://IP地址:5001/webapi/auth.cgi?api=SYNO.API.Auth&method=Login&version=1&account=登陆用户名&passwd=登陆密码
```

浏览器输入如下地址，显示如下信息即可进行下一步：（IP地址替换为NAS的地址，序列号就是刚才信息中心的产品序列号）

```
https://IP地址:5001/webapi/entry.cgi?api=SYNO.ActiveBackup.Activation&method=set&version=1&activated=true&serial_number="序列号"
```

这样我们就完成了Active Backup for Business套件的激活，打开正常

内网连接一下，没有问题

接下来就是一个要非常注意的问题了，黑群用户由于没有QC所以需要做端口映射或者内网穿透才能在公网访问到NAS

这里大家注意，一定要把 **5510** 端口映射（TCP）出去，要不你在外网的机器上使用Active Backup for Business套件连接NAS的时候会提示没有网络连接

如果你使用的frp进行内网穿透的话，客户端就需要如下配置，有公网IP的用户直接在路由器上做端口映射就行了

这样我们就可以在公网连接使用Active Backup for Business套件了

这样我们就完成了黑群晖 Active Backup for Business 套件的激活，并且在内网和公网都能够正常连接



## 群晖7.X激活方法如下：

```
https://群晖地址:5001/webapi/auth.cgi?api=SYNO.API.Auth&version=3&method=login&account=管理员用户名&passwd=密码&format= cookie
```

然后网页提示中有"success":ture字样就是OK了 注意： 

1、群晖的https是5001端口

2、密码中只包含字母和数字，如果存在特殊符号，大概需要转换，按哪个标准我就不知道了

​      懒得纠结的就去把密码改一下，回头改回来就行

3、cookie前有个空格，别忘了

然后在网页中输入以下网址：

```
https://群晖地址:5001/webapi/entry.cgi?api=SYNO.ActiveBackup.Activation&method=set&version=1&activated=true&serial_number="序列号"
```

将网址中的地址和序列号替换

当success为true同时activated为true时说明激活成功，进入DSM，ABB顺利打开



## 在线激活：

http://mi-d.cn/d/ABB.html 支持浏览器[firefox](https://423down.lanzouo.com/b0f3f48yf)、[theworld6](http://download.theworld.cn/ver/TWInst_6.2.0.128.exe)、[theworld7](http://download.theworld.cn/ver/TWInst_7.0.0.108.exe) 其他浏览器不支持


