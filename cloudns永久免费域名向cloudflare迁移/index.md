# ClouDNS永久免费域名向cloudflare迁移




 上一篇文章已经教大家如何白嫖一个ClouDNS免费服务下的永久域名，见[教你免费注册一个ClouDNS永久域名(保姆级教程）](https://www.wenjie1018.cn/%E6%95%99%E4%BD%A0%E5%85%8D%E8%B4%B9%E6%B3%A8%E5%86%8C%E4%B8%80%E4%B8%AAcloudns%E6%B0%B8%E4%B9%85%E5%9F%9F%E5%90%8D/)

  现在再来教大家如何将ClouDNS账户下的域名迁移到cloudflare上，方便大家充分利用cloud flare提供的免费SSL证书、DDOS保护、DNS解析、网页防火墙、CDN加速等服务。



## 01准备工作

前提：

注册好一个cloudflare账号（网上有教程）

注册好一个ClouDNS账号并注册域名，见教程[教你免费注册一个ClouDNS永久域名(保姆级教程）](http://mp.weixin.qq.com/s?__biz=MzkyNzYzNDEzMA==&mid=2247483919&idx=1&sn=2d4098e3207688b3c6a4c1a65ad69b85&chksm=c22445b2f553cca4b58f08c6d487c8bbfeff90b63b28552b988ac9dca047481c81e2cb7a2e79&scene=21#wechat_redirect)

登录cloudflare 网址：https://dash.cloudflare.com/login



{{< image src="./a3b8ca68a882066ed5375ca00dde1755.png">}}



登录cloudns 网址：https://www.cloudns.net/index/show/login/



{{< image src="./8a8356d27cbf9811d40839288c7ce931.png">}}



## 02迁移



1.cloudns中双击域名进入解析列表

点击删除符号，删除已有的NS记录



{{< image src="./cee2f5bc13afb8b166549493fc489b6d.png">}}



2.cloudflare点击添加站点



{{< image src="./b96d715628ed0f9558b156c43b9d198a.png">}}



3.输入你的cloudns域名，点击继续



{{< image src="./3031a613e4b1601f786f6f252783d63b.png">}}



3.三步骤

步骤一：下拉选择Free计划，点击继续



{{< image src="./609ca360f2b654b1eb2384d6773e9ebe.png">}}



步骤二：扫描DNS记录，点击继续，再点击确认



{{< image src="./8b0b0c6dc2dd8085d2c83caffd6244ac.png">}}



步骤三：更改服务器名称，下拉到第三小点查看为我们分配到的名称服务器，先复制第一个



{{< image src="./c7dcab01cf0729442688008ecc39ecf2.png">}}



切换到cloudns，它的NS记录已经在之前的操作中删除了，点击添加新记录



{{< image src="./c7dcab01cf0729442688008ecc39ecf2.png">}}



类型选择NS，指向到粘贴我们在cloud flare复制的第一个名称服务器地址（例如我的是julissa.ns.cloudflare.com），点击保存



{{< image src="./94a11942e22b633d2c73d5d29bf2f413.png">}}



重复刚刚的操作将cloud flare复制的第二个名称服务器地址也添加进去



{{< image src="./b1f41ea291d30e2a7725cefbe7aae583.png">}}



4.切换回cloud flare的三步骤，在第三步骤处下拉，选择继续



{{< image src="./43c03bf8b65d45f0d67e67f90161a991.png">}}



点击开始使用



{{< image src="./dd0e5b1ea99d37195f3f5e8c7bceef68.png">}}



一路点击保存，最后点击完成



{{< image src="./e34a485c8502fed04a52e8db6c81ce99.png">}}



跳转页面后下拉，点击立即检查名称服务器



{{< image src="./a95eed6d61905bf86b30902c5bb3b4f4.png">}}



{{< image src="./e9464e7d0bba7a033137b8ba80fd8ddc.png">}}



至此已经全部结束了，耐心等待几十分钟或者几小时即可，完成时一般会邮件提醒。

那么，从现在起你就有了能够很好利用cloud flare各项免费服务的基础，各种探索去吧。


