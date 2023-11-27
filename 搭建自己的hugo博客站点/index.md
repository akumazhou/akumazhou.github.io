# 搭建自己的hugo博客站点


## 实验环境
```
win10
git version 2.17.0.windows.1
hugo v0.98.0
```
<br>

## hugo官网
https://gohugo.io/
<br>

## hugo安装
### 1.安装git
[实战：git安装](https://blog.csdn.net/weixin_39246554/article/details/124569192?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22124569192%22%2C%22source%22%3A%22weixin_39246554%22%7D&ctrtid=mr1mD)
————————————————
版权声明：本文为CSDN博主「一念一生～one」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_39246554/article/details/124573538

<br>

### 2.安装hugo

 - 打开hugo下载链接，直接下载go二进制安装包：

https://github.com/gohugoio/hugo/releases/download/v0.102.3/hugo_extended_0.102.3_Windows-64bit.zip

 - 将下载的go二进制安装包放到自己电脑某个目录下，然后将其路径放到自己电脑的环境变量下(自己配置目录为D:\SoftInstall\hugo)


 - 配置环境变量具体步骤如下：
win + R，输入：`sysdm.cpl`快速打开pc的环境变量配置：
1.点击高级

2.环境变

3.找到Path那一行，点击编辑
4.点击新建，然后输入刚才下载的二进制目录所在路径(自己配置目录为D:\SoftInstall\hugo)，点击确认：
5.全部确认即可

至此，hugo的环境变量就配置好了，我们打开`cmd`，输入`hugo version`查看是否有效果：
![2023-11-21T09:27:50.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/1372287443.png)
有结果输出，表示hugo安装正常。

<br>

### 3.本地预览

 - 1.创建本地站点根目录

   打开Git Bash，来到`D:\`目录下，然后输入如下命令，进行创建本地站点根目录：（运行`$`后的代码）

   ```
   $ hugo new site hugoblog
   Congratulations! Your new Hugo site is created in D:\hugoblog.
   
   Just a few more steps and you're ready to go:
   
   1. Download a theme into the same-named folder.
      Choose a theme from https://themes.gohugo.io/ or
      create your own with the "hugo new theme <THEMENAME>" command.
   2. Perhaps you want to add some content. You can add single files
      with "hugo new <SECTIONNAME>\<FILENAME>.<FORMAT>".
   3. Start the built-in live server via "hugo server".
   
   Visit https://gohugo.io/ for quickstart guide and full documentation.
   
   
   hg@LAPTOP-G8TUFE0T MINGW64 /d
   $ cd hugoblog/
   
   hg@LAPTOP-G8TUFE0T MINGW64 /d/hugoblog
   $ ls
   archetypes/  config.toml  content/  data/  layouts/  public/  static/  themes/
   
   hg@LAPTOP-G8TUFE0T MINGW64 /d/hugoblog
   ```

   

 - 2.下载hugo主题

   因为hugo没有内置主题，所以你需要去下载一个：

   配置文件为：hugo.toml

   ```
   hg@LAPTOP-G8TUFE0T MINGW64 /d/hugoblog
   $ git clone https://github.com/reuixiy/hugo-theme-meme.git themes/meme
   Cloning into 'themes/meme'...
   remote: Enumerating objects: 5583, done.
   remote: Counting objects: 100% (740/740), done.
   remote: Compressing objects: 100% (289/289), done.
   remote: Total 5583 (delta 507), reused 451 (delta 451), pack-reused 4843
   Receiving objects: 100% (5583/5583), 9.31 MiB | 12.59 MiB/s, done.
   Resolving deltas: 100% (3086/3086), done.
   
   hg@LAPTOP-G8TUFE0T MINGW64 /d/hugoblog
   $ rm config.toml && cp themes/meme/config-examples/en/config.toml hugo.toml
   ```

   继续按说明添加那两个页面：

   ```
   hugo new "posts/hello-world.md"
   hugo new "about/_index.md"
   ```

   然后将上述两个文件中的草稿字段（ draft ）改为 false：

   ```
    title: "Hello World"
    date: 2021-07-20T01:53:48Z
    draft: false
   ```

 - 3.创建第一个测试文件

   ```
   hg@LAPTOP-G8TUFE0T MINGW64 /d/hugoblog
   $ hugo new posts/first.md
   Content "D:\\hugoblog\\content\\post\\first.md" created
   
   hg@LAPTOP-G8TUFE0T MINGW64 /d/hugoblog
   $ echo "i love you,xyy hurt!" >> content/post/first.md
   ```

   

 - 🍀 说明

   ```
   hugo new [路径]文章名.md
   hugo new会创建包含默认元数据的文章，如果没有路径, 文章会保存在content目录中。
   
   md的文章会在开始部分添加元数据,
   数据格式为 yaml toml json格式如下:
   
   +++
   
   title = "my first blog"
   date = "2019-10-28T09:38:35+08:00"
   draft = true
   
   +++
   
   markdownz正文部分>>>
   PS:
   draft=true表示文章默认为草稿
   draft=false 才能识别非草稿
   ```

   

 - 4.本地预览

   ```
   $ hugo server -v -D
   
   #hugo -d 目标路径
   不指定目标路径, 会默认在public目录下生成可部署的网站.
   我们通过hugo server -D本地生成网站预览. 他会监控页面的更改, 并刷新页面.
   ```

   在浏览器打开如下链接，http://localhost:1313/ 观察效果：
![2023-11-22T02:42:08.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/1962752334.png)
完美。😘



## 推送到github并设置公网可访问

### 1.github上创建仓库

登录github：https://github.com/

点击`Your repositories`：

![2023-11-22T02:43:12.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/3204874867.png)

点击`new`：

![2023-11-22T02:43:40.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/3661351239.png)

填写仓库名，选择`Public`，添加一个Readme文件：

![2023-11-22T02:44:20.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/1665340691.png)

点击`Create respository`：

![2023-11-22T02:44:41.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/3340248009.png)

完成仓库创建。

### 2.将本地文件推送到远程仓库

 - 此时，来到博客根目录，先执行下hugo -D生成下网站所需数据：

   ```
   $ hugo -D
   ```
   此时，你能看到public目录下，生成可很多文件，这个就是后续生成网站所需要的数据。

![2023-11-22T02:48:25.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/775782341.png)

 - 此时，来到public目录下，执行如下命令

```
$ cd public/

$ git init
$ git remote add origin git@github.com:OnlyOnexl/hugoblog.git
$ git add .
$ git commit -m"first commit"
$ git push  --set-upstream origin master
$ gs
```




![2023-11-22T02:48:37.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/1894604204.png)

🍀 关于这里如何配置git客户端到github的公私钥方法，请看如下方法：

Git配置ssh登录GitHub管理自己的代码

检测本地pc是否已存在ssh秘钥(不存在可忽略次步骤)

![2023-11-22T02:50:12.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/3176942945.png)


#### 1️⃣ `设置签名`

右键单击鼠标，点击 Git Bash Here输入以下命令，设置签名：

   ```
git config --global user.name  "hg"
git config --global user.email  "2675263825@qq.com"
   ```

#### 2️⃣ `生成ssh秘钥`

然后生成密钥(公钥和私钥)：

   ```
ssh-keygen -t rsa -C "2675263825@qq.com"

#备注：
1.过程中按2次回车就好；
2.也可以添加-b选项 # ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```

![2023-11-22T02:54:15.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/2007847329.png)

#### 3️⃣ `复制ssh公钥到github`

现在密钥已经生成，一般存放在（/c/Users/you/.ssh/id_rsa.pub.），我们运行下面的命令将密钥复制为粘贴板，等会儿会粘贴到github上去：

![2023-11-22T02:55:55.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/2638915209.png)

![2023-11-22T02:56:01.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/3309677345.png)

复制 id_rsa.pub 文件内容，登录 GitHub，点击用户头像→Settings→SSH and GPG keys，New SSH Key，输入复制的密钥信息，保存：

![2023-11-22T02:56:16.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/2673046767.png)

![2023-11-22T02:56:25.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/4143490167.png)

#### 4️⃣ 验证：本地连接Github

右键单击鼠标，点击 Git Bash Here输入以下命令，如果如下图所示，出现你的用户名，那就成功了

   ```
$ ssh -T git@github.com
   ```
![2023-11-22T02:57:09.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/3819990255.png)

 - 此时来到github仓库下，观看数据已经被推送上来了：

![2023-11-22T02:57:36.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/4221396841.png)

最后记得在github上设置下gitpages功能

点击`Settings`，`Pages`:

![2023-11-22T02:58:23.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/3941394697.png)

选择`master`分支，点击`Save`：
![2023-11-22T02:58:47.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/3801776621.png)

 - 验证效果：

公网访问：

https://onlyonexl.github.io/hugoblog/


#### 5️⃣ 如何自定义域名

 - 购买域名
 - 配置域名解析
 - 配置GitHub Pages

![2023-11-22T03:02:16.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/978785839.png)

 - 验证

公网访问域名：http://www.onlyyou520.com/

![2023-11-22T03:02:47.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/232267345.png)

大功告成，接下来就可以开心写自己博客了！😘


### 3.hugo进阶
📍 如何为某篇文章打上标签及分类？
当然实际上，Hugo默认会产生 tags 和 categories 的分类，如果只需要这两个，可以不用在 config.toml 中声明就在post头部使用。

 - 配置方法

   ```
   
   title: "First"
   date: 2022-05-03
   tags: ["hugo"]
   categories: ["hugo"]
   
   ```
   📍 如何一键发布自己写好的文章到github？

 - 配置方法

   ```
   $ vim /etc/profile
   alias hg="cd /d/hugoblog/ && hugo -D && cd /d/hugoblog/public && git add -A && git commit -m 'empty' && git push"
   $ source /etc/profile
   ```

这里利用了shell脚本进行一键发布哈哈！😘

 - 测试效果

在content/post目录下创建新文件：
![2023-11-22T03:09:45.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/2544668146.png)
一键发布：
![2023-11-22T03:09:59.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/1590257231.png)

![2023-11-22T03:10:33.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/2919408003.png)

![2023-11-22T03:11:06.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/282804715.png)

📍 注意：本地仓库推送到github，数据是有一定延时的！😥

📍 如何解决文章后关于Author及Link信息？\

 - 问题现象

![2023-11-22T03:46:52.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/2096459959.png)

 - 解决办法

默认配置：
![2023-11-22T03:47:19.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/1580723510.png)

![2023-11-22T03:47:29.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/1178313654.png)

修改后配置：
![2023-11-22T03:47:56.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/1815973137.png)

![2023-11-22T03:48:02.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/1216972174.png)

 - 验证(完美)😘

![2023-11-22T03:48:29.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/4290606701.png)

📍 如何修改站点名称(已解决)-2022.5.4

 - 修改方法
   ```
   title = "Onlyyou"
   ```
   ![2023-11-22T03:49:16.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/2062306389.png)

 - 效果

![2023-11-22T03:49:34.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/2844540220.png)

📍 hugo目录结构

![2023-11-22T03:49:54.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/858327912.png)

   ```
hg@LAPTOP-G8TUFE0T MINGW64 /d
$ cd hugoblog/

hg@LAPTOP-G8TUFE0T MINGW64 /d/hugoblog
$ ls
archetypes/  config.toml  content/  data/  layouts/  public/  static/  themes/
1. config.toml
    所有的hugo站点都有一个全局配置文件，用来配置整个站点的信息，hugo默认提供了跟多配置指令。
2. content
    站点下所有的内容页面，也就是我们创建的md文件都在这个content目录下面。
3. data
    data目录用来存储网站用到一些配置、数据文件。文件类型可以是yaml|toml|json等格式。
4. layouts
    存放用来渲染content目录下面内容的模版文件，模版.html格式结尾，layouts可以同时存储在项目目录和themes//layouts目录下。
5. static
    用来存储图片、css、js等静态资源文件。
6. themes
    用来存储主题，主题可以方便的帮助我们快速建立站点，也可以方便的切换网站的风格样式。
7. public
    hugo编译后生成网站的所有文件都存储在这里面，把这个目录放到任意web服务器就可以发布网站成功
8. archetypes  
    Hugo new 创建内容页面的时候预置的内容模板
   ```

📍 如何安装新的hugo主题(已解决)-2022.5.4
🍀 一般情况下，将主题克隆下来放到themes目录下就可以

🍀 但有的主题，需要把config.toml给替换掉，例如meme主题：

   ```
hg@LAPTOP-G8TUFE0T MINGW64 /d/hugoblog
$ git clone https://github.com/reuixiy/hugo-theme-meme.git themes/meme #将主题克隆并重命名到themes目录即可！
Cloning into 'themes/meme'...
remote: Enumerating objects: 5583, done.
remote: Counting objects: 100% (740/740), done.
remote: Compressing objects: 100% (289/289), done.
remote: Total 5583 (delta 507), reused 451 (delta 451), pack-reused 4843
Receiving objects: 100% (5583/5583), 9.31 MiB | 12.59 MiB/s, done.
Resolving deltas: 100% (3086/3086), done.

hg@LAPTOP-G8TUFE0T MINGW64 /d/hugoblog
$ rm config.toml && cp themes/meme/config-examples/en/config.toml config.toml
   ```
📍 如何取消GitHub Pages功能(已解决)-2022.5.4

 - 故障现象：在关闭这个GitHub Pages功能时报错

![2023-11-22T03:55:34.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/506951495.png)

 - 解决办法

![2023-11-22T03:55:49.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/3089627671.png)

本次直接删除仓库了：

![2023-11-22T03:56:09.png](https://wenjie1018.cn:8001/usr/uploads/2023/11/352935857.png)

[实战：手把手带你从0到1搭建自己的hugo博客站点(持续更新)-2022.5.4](https://blog.csdn.net/weixin_39246554/article/details/124573538)
