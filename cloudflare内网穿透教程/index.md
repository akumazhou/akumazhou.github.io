# CloudFlare内网穿透教程




## CloudFlare内网穿透

{{< figure src="./91d3d662b5879c379aafcfcf2ee445de.png" >}}

> 1. 内网穿透：让其他人可以通过公网访问到内网服务；
> 2. CloudFlare免费提供内网穿透服务和HTTPS服务，但是需要拥有一个属于自己的域名；
> 3. CloudFlare官网：https://www.cloudflare-cn.com/
> 4. CloudFlare内网穿透三部曲
>
> - 买域名：购买一个域名，并将其DNS服务器设置为CloudFlare提供的DNS服务器（即将域名托管到CloudFlare）；
> - 建隧道：在CloudFlare上创建一个隧道（CloudFlare本质上给我们提供了一个公网IP地址和服务器，但是需要配置隧道连接）；
> - 连隧道：下载CloudFlare提供的隧道客户端，并在本地通过客户端连接上CloudFlare提供的服务器（相当于通过一根虚拟网线，将我们的电脑与云服务器直连了）。

### 第一次使用

1. 新注册的账号首次登陆

{{< figure src="./5132b8f0b8fdac3d2e5fa849a265c056.png" >}}

2. 添加域名

{{< figure src="./9957e091992e206ad1f63743c61848a5.png" >}}

3. 选择免费服务

{{< figure src="./d75b29e3ba9603b30a7c0e5c22687dc4.png" >}}

4. 更改域名解析服务器

{{< figure src="./11067aecd0b98c34ef2d05f0532fda4e.png" >}}

5. 回到主页，检查是否成功

{{< figure src="./84a32188770565efdcfbcf3dfcacc6af.png" >}}

6. 在首页中，进入Zero Trust

{{< figure src="./ae47ebe7aea60ada139530acb3e1425b.png" >}}

7. 随便写个名字

{{< figure src="./52e14532e98838ee4ef9ae26dbf21d5c.png" >}}

8. 选择免费的服务

{{< figure src="./18def01f3970420b085b2820b8cd1ef0.png" >}}

9. 点击继续

{{< figure src="./f004a12b742b9e658256a9c7809d1b00.png" >}}

10. 直接回到首页

{{< figure src="./8ca0640cd6abec8224a040943d3f0616.png" >}}

11. 在进入ZeroTrust，见第六步

12. 进入Tunnels

{{< figure src="./94174f598ae65984bf996d4310bc23b1.png" >}}

13. 添加一条隧道

{{< figure src="./8de675d20acc8464488a1dee3ad6497d.png" >}}

14. 选择第一个方式

{{< figure src="./d518a237a51d2516f3eb89f614cf9d34.png" >}}

15. 给隧道随便起个名字

{{< figure src="./eda83d758950c24bb54ccbc0fafd7fba.png" >}}

16. 下载客户端软件

{{< figure src="./b97f51ce66f8f6d01c0f6e95d99d2d49.png" >}}

17. 出现下面这个界面则说明你自己的电脑连接上了cloudflare服务器上面的隧道

{{< figure src="./e29439d99da8c0775fc1fc743c7374e7.png" >}}

18. 配置路由

{{< figure src="./4f21788af7bffeb22f154113f23703fc.png" >}}

{{< figure src="./ad15efa660b67becc88436d89ed431eb.png" >}}

{{< figure src="./27d0cf96d825c7ef76d05dd064e76baa.png" >}}

{{< figure src="./fd31c984cc58a303e922cae620e60536.png" >}}

19. 启动服务

{{< figure src="./cc916fd747bc38fb6e7811f0813d884f.png" >}}

{{< figure src="./001481c826007c94ef667ffebbeef4ea.png" >}}

### 再次连接

1. 断开隧道连接的两种方式

   - 电脑重启

   - 手动断开

     ``` 
     cloudflared.exe service uninstall
     ```

2. 在电脑重启之后，云服务器就没办法将流量转发到我们的电脑上，同样我们也无法将结果响应给云服务器，因此如果你之前创建了一个隧道，但现在断开了，就需要重新连接。

3. 重新连接需要两步：释放客户端之前的隧道连接、重新连接服务器隧道

4. 释放之前的客户端连接

   ```
   cloudflared.exe service uninstall
   ```

{{< figure src="./c803ef55f647fd8ddbc6279926bccf34.png" >}}

5. 重新连接服务器隧道

   - 进入到第一次使用中的16步所在页面，点击刷新token（Refresh token）

{{< figure src="./c4d722458249860f4ce0bc24538b3518.png" >}}

   - 复制命令，到命令行窗口中执行

{{< figure src="./9b6112a3576c9ef0989ea786064ede3b.png" >}}

