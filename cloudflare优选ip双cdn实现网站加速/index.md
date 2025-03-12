# CloudFlare优选IP，双CDN实现网站加速




# CloudFlare优选IP，双CDN实现网站加速

> 随着全球化的不断深入，越来越多的企业和组织开始关注如何提升其网站在不同地区的访问速度和稳定性。其中，内容分发网络（Content Delivery Network, CDN）作为一种有效的解决方案，已经被广泛应用。然而，单一的CDN服务可能无法满足全球范围内的访问需求，特别是在跨国访问时，可能会遇到延迟和稳定性问题。因此，双CDN策略应运而生，通过结合国内外两个CDN服务，实现更高效的内容分发和访问优化。

### 一、CDN的基本概念

CDN是一种分布式网络服务，其核心思想是将内容缓存到离用户更近的服务器上，从而减少数据传输的延迟，加快内容加载速度。CDN通常由多个分布在不同地理位置的节点组成，这些节点可以是数据中心、边缘服务器或者云服务。

### 二、双CDN分流的工作原理

双CDN分流是指同时使用两个CDN服务，一个服务覆盖国内用户，另一个服务覆盖国外用户，实现全球加速访问。

### 三、准备工作

1、需要准备两个域名，以我的为例；

- www.geeklinux.cn 网站主要域名（使用阿里云或者腾讯云dns云解析）
- example.com 次要域名，DNS服务器需设置为CloudFlare

2、PayPal账号或者Visa信用卡一张

3、服务器一台

4、CloudFlare账号



### 四、配置CloudFlare

登录你的CloudFlare账号（没有就去注册），将你的次要域名DNS提供商接入到CloudFlare中。

在DNS解析中添加一条记录，如`cloudflare.example.com`，指向源服务器，并启用CloudFlare的CDN加速（即开启小黄云图标）。

在SSL/TLS设置中，选择“自定义主机名”，并绑定PayPal账号或双币信用卡以使用该功能。

添加回退源，填写指向源服务器的域名（例如`cloudflare.example.com`）。

{{< figure src="./640.png" >}}

将你的网站（www.geeklinux.cn）添加一条记录，线路选择境外，如下图所示

{{< figure src="./641.png" >}}



添加完成后回到CloudFlare  自定义主机名，添加自定义主机名，添加上你的网站（www.geeklinux.cn）

{{< figure src="./642.png" >}}



添加相应的TXT记录，等待状态变为有效即可，效果如下图

{{< figure src="./643.png" >}}

### 五、配置CloudFlare优选IP

CloudFlare默认解析出的节点IP国内访问不佳,甚至无法打开，这时候我们需要通过优选IP将服务器解析到国内访问CloudFlare速度最快的节点即可（因为CloudFlare通过Anycast泛播/任播）技术实现的CDN加速，所以只要是他节点中的IP地址都可以正常访问您的网站。

可以直接用我的地址 cf.geeklinux.cn CNAME到你的网站中即可，也可以通过一些工具来判断哪些IP访问速度最快，这里我推荐麒麟域名监测：https://api.uouin.com/cloudflare.html，来识别访问速度最快的IP。

优选IP之后的访问测速

{{< figure src="./644.png" >}}

**注意：在自定义主机名成功验证之前，不能配置使用优选IP地址，否则检查将会失效，造成无法访问。**

**另外不能使用单域名配置回退源，否则会被CloudFlare拉平。**
