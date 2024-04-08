# 阿里云服务器ECS搭建个人网站新手教程（超详细）




> **简介：** 阿里云服务器ECS搭建个人网站新手教程超详细，使用阿里云服务器快速搭建网站教程，先为云服务器安装宝塔面板，然后在宝塔面板上新建站点，阿里云服务器网以搭建WordPress网站博客为例，来详细说下从阿里云服务器CPU内存配置选择、Web环境、域名解析到网站上线全流程：

使用阿里云服务器快速搭建网站教程，先为云服务器安装宝塔面板，然后在宝塔面板上新建站点，阿里云服务器网以搭建WordPress网站博客为例，来详细说下从阿里云服务器CPU内存配置选择、Web环境、域名解析到网站上线全流程：

# 步骤一：云服务器配置选择

如果你已经有了阿里云服务器，那么可以跳过步骤一。阿里云服务器分为[云服务器ECS](https://www.aliyun.com/product/ecs?source=5176.11533457&userCode=r3yteowb)和[轻量应用服务器](https://www.aliyun.com/product/swas?source=5176.11533457&userCode=r3yteowb)，轻量应用服务器支持WordPress、宝塔面板等应用镜像，通过应用镜像可以一键搭建网站，非常简单，所以阿里云服务器网就不多赘述。本文阿里云服务器网是以云服务器ECS实例为例，从零开始为大家讲解使用阿里云服务器建站流程。

关于轻量和ECS区别请参考：[https://help.aliyun.com/document_detail/369471.html](https://help.aliyun.com/document_detail/369471.html?source=5176.11533457&userCode=r3yteowb) 本文不多赘述。

云服务器CPU内存配置如何选择？根据实际应用情况选择，如果是个人用户搭建博客1核2G或2核2G就够用了，如果是企业用户建议2核4G起步，阿里云服务器网用来搭建个人博客，所以选择了1核2G配置的云服务器，1M公网带宽就够用了，操作系统选择了CentOS镜像。可以使用阿里云测速工具 aliyunping.com 测试一下本地到阿里云服务器各个地域节点的Ping值网络延迟。

- 云服务器ECS：[https://www.aliyun.com/product/ecs](https://www.aliyun.com/product/ecs?source=5176.11533457&userCode=r3yteowb)
- 轻量应用服务器：[https://www.aliyun.com/product/swas](https://www.aliyun.com/product/swas?source=5176.11533457&userCode=r3yteowb)

# 步骤二：通过宝塔面板为云服务器安装Web环境

Web环境是网站运行所依赖的环境，阿里云百科是用来搭建WordPress博客，为云服务器安装LNMP环境（Linux+Nginx+MySQL+PHP），本文的LNMP环境是通过安装宝塔Linux面板实现的，下面开始安装宝塔Linux面板。

## 1、SSH连接登录到云服务器

阿里云服务器支持多种远程连接方式，可以使用阿里云自带的[Workbench远程连接方式](https://help.aliyun.com/document_detail/71529.html?source=5176.11533457&userCode=r3yteowb)，也可以使用第三方SSH远程连接软件如PuTTY、Xshell等。阿里云服务器网使用阿里云自带的远程连接方式：

首先登录到云服务器ECS管理控制台，左侧栏【实例与镜像】>>【实例】，找到目标云服务器ECS实例，然后点击右侧的【远程连接】，如下图：

{{< image src="./gwu3lhygmapgi_7f2a540201554efca023f04b21b76ae5.jpg" caption="图片1" >}}

可以选择SSH密码登录或密匙证书登录，如果没有密码，可以[重置密码](https://help.aliyun.com/document_detail/25439.html?source=5176.11533457&userCode=r3yteowb)。

## 2、执行宝塔面板的安装命令

登录到你的云服务器后，执行宝塔面板安装命令，阿里云服务器网使用的CentOS操作系统，命令如下：

```
yum install -y wget && wget -O install.sh https://download.bt.cn/install/install_6.0.sh && sh install.sh ed8484bec
```

执行宝塔Linux面板安装命令后，会提示如下：

```
Do you want to install Bt-Panel to the /www directory now?(y/n): y
```

保持默认，回复个字母“y”，如下图：

{{< image src="./gwu3lhygmapgi_587a0b985252458d9d93f9b9846bbf7e.jpg" caption="图片2" >}}

然后回车，系统会自动安装，大约1分钟左右会自动安装完成。

## 3、宝塔面板登录地址、账号和密码

宝塔面板自动安装完成后，会显示宝塔后台登录地址、username和password，如下图：

{{< image src="./gwu3lhygmapgi_2052ebb6352b46f3aa789e8846311ad8.jpg" caption="图片3" >}}
如上图所示，保存好上述信息，如果是通过外网登录宝塔后台，就是用外网面板地址，如果是在云服务器上登录宝塔可以使用内网面板地址。

## 4、在阿里云服务器控制台开通宝塔面板端口

最初宝塔面板的端口号是8888，出于安全考虑，现在宝塔面板使用的端口是程序安装完成后随机生成的端口号，在上图的面板地址中可以看出，端口号为39118，在云服务器ECS的安全组中开启宝塔端口号。

安全组开启端口详细教程参考：[https://help.aliyun.com/document_detail/25471.html](https://help.aliyun.com/document_detail/25471.html?source=5176.11533457&userCode=r3yteowb)

## 5、登录到宝塔管理地址并安装LNMP环境

在浏览器中粘贴宝塔面板的外网面板地址，并输入账号和密码，登录到宝塔面板管理后台，第一次登录需要勾选同意协议，然后进入面板。然后绑定宝塔帐号，有宝塔账号的话，直接输入手机号和密码登录即可。

然后会弹出推荐安装套件窗口，选择LNMP(推荐)，点击【一键安装】，如下图：

{{< image src="./gwu3lhygmapgi_d9fb80055cc14b86b0bd8fe36915d11e.jpg" caption="图片4" >}}

会弹出消息盒子，显示安装进度，大约等待5分钟左右，即可自动安装WordPress博客程序所需的Web环境。

# 步骤三：在宝塔面板上添加站点

登录到宝塔面板管理后台，点击左侧栏的【网站】>>【添加站点】，如下图：

{{< image src="./gwu3lhygmapgi_ad7df6da40994b7f90558685d096fa88.jpg" caption="图片5" >}}
域名：输入域名，www和不带www都的域名均可填写
根目录：根目录会根据域名自动生成，默认即可
FTP账号：需要FTP就选择创建，系统会自动生成FTP账号和密码，也可以自己自定义设置
数据库：选择创建MySQL，系统会自动创建数据库账号和密码

然后点【提交】，会显示成功创建站点，并显示FTP和数据库账号资料。

# 步骤四：下载WordPress程序安装包

已经下载的同学可以跳过此步骤，在WordPress官网下载WP程序安装包即可。

# 步骤五：上传WordPress安装包到根目录

点击左侧栏【文件】>>【上传】，将你的WordPress安装包程序上传到网站根目录。网站根目录路径为：/www/wwwroot/你的域名，如下图：

{{< image src="./gwu3lhygmapgi_f1746b01365d40739a9e045cbc656df8.jpg" caption="图片6" >}}

# 步骤六：域名解析到你的云服务器公网IP地址

在域名注册商处，将你的域名解析到你的云服务器的公网IP地址上，解析教程以域名注册商文档为准，阿里云域名添加网站解析参考：[https://help.aliyun.com/document_detail/106535.html](https://help.aliyun.com/document_detail/106535.html?source=5176.11533457&userCode=r3yteowb)

# 步骤七：安装WordPress程序

域名解析到云服务器生效后，在浏览器中输入你的域名，并打开网站，就可以看到熟悉的WordPress安装界面，如下图：

{{< image src="./gwu3lhygmapgi_1696a62d1b2945feb9e8c98b7b574530.jpg" caption="图片7" >}}
如上图，点击现在就开始！
填写数据库名、数据库用户名和密码信息，该信息是在步骤三中，在宝塔面板上添加站点时生成的用户名和密码信息，此步骤填写的是数据库信息，填写完成后点击提交。如下图：

{{< image src="./gwu3lhygmapgi_e70ecfe04f194cfba4b18acf1344e206.jpg" caption="图片8" >}}

数据库信息通过后，然后填写WordPress站点标题、用户名、密码及电子邮件信息，然后点击安装WordPress，如下图：

{{< image src="./gwu3lhygmapgi_cbd3fbb29fc04bb7829b8cdf3a09c69c.jpg" caption="图片9" >}}
提示：成功！WordPress安装完成。谢谢！

{{< image src="./gwu3lhygmapgi_52f8071921ac49239f85f0eb58aa17fd.jpg" caption="图片10" >}}

至此，使用阿里云服务器搭建WordPress网站博客教程完毕，现在云服务器安装WordPress所需的Web环境，本文阿里云百科选择通过宝塔面板的方式来安装Web环境，然后在宝塔面板上新建WordPress网站。

更多关于阿里云服务器使用说明，请以官方页面为准：[https://www.aliyun.com/product/ecs](https://www.aliyun.com/product/ecs?source=5176.11533457&userCode=r3yteowb)



<br>

————————————————<br>
版权声明：本文为CSDN博主「生生世世是所说的」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：[阿里云服务器ECS搭建个人网站新手教程（超详细）-阿里云开发者社区 (aliyun.com)](https://developer.aliyun.com/article/1209096)
