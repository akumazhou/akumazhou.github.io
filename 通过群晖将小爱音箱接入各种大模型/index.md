# 通过群晖将小爱音箱接入各种大模型




# 通过群晖将小爱音箱接入各种大模型



在上篇文章中我们把[群晖](https://pinpai.smzdm.com/2315/)接入了各大模型，接口实现了 API 接口的统一。 

很多小伙伴不知道接入了有什么作用，其最大的优势就是统一了不同厂家的API接口。

为什么要统一呢？

因为现在很多软件或项目都要用这个统一后的标准API接口。比如今天要说的把[小爱](https://www.smzdm.com/ju/spx8kr0/)[音箱](https://www.smzdm.com/fenlei/yinxiang/)接入各中大语言模型，就要用到统一后的API接口。

把小爱音箱接入大语言模型后，家里的小朋友就可以直接对着音箱问《十万个为什么》了，解放你的大脑和嘴。我们也可以利用大模型第三方接口功能，进行实时资讯的获取。

你可能有疑问，如果要把小爱音箱接入的话大模型是不是要刷机改硬件？不，它非常简单。



## 项目地址

https://github.com/idootop/mi-gpt

## 功能

- **问答**。想象一下，当小爱音箱接入大模型后，上知天文，下知地理，从“人工智障”秒变学霸。
- **角色扮演**。一秒调教小爱，无论是成为你的完美伴侣，还是那个能听你倾诉心事的贴心闺蜜，都不在话下。
- **流式响应**。爱情来得太快就像龙卷风，而你的小爱音箱也是，对你的爱意秒回，爱你不会让你等太久。
- **长短期记忆**。小爱音箱现在能记住你们之间的每一次对话，越聊越默契，就像是你身边的老朋友。
- **自定义 TTS**。厌倦了[小爱同学](https://www.smzdm.com/ju/swm8xrv/)的语音？帮你解锁[「豆包」](https://www.doubao.com/)同款音色，就像真人在回你的消息。

## 配置文件

在安装项目之前，我们要准备好两个配置文件。

🔻 浏览器打开 https://github.com/idootop/mi-gpt[，下载env、migpt两个配置文件。](https://github.com/idootop/mi-gpt)

{{< figure src="./66b43c69e4e033406.png_e1080.jpg" >}}

🔻 下载完毕后，修改 migpt 文件的内容。需要在米家中找到userId，did 为米家中音箱显示的名称，建议重新命名，最好去掉空格，然后复制粘贴进来。

{{< figure src="./66b43c67cf5973250.png_e1080.jpg" >}}

🔻 接着往下，在 migpt 文件中找到tts指令，点击上面的链接，根据自己的音箱型号找到对应的指令并填入。

{{< figure src="./66b43c6930cf03406.png_e1080.jpg" >}}

{{< figure src="./66b43c69a548d3406.png_e1080.jpg" >}}

🔻 修改 env 文件的内容，把上篇文章中搭建好URL地址和MODEL填入。

{{< figure src="./66b43c698784d3406.png_e1080.jpg" >}}

🔻 把两个文件上传到群晖中。

{{< figure src="./66b43c68588045517.png_e1080.jpg" >}}

🔻 为了方便后期修改，建议把文件进行重命名。

{{< figure src="./66b43c671e37f3250.png_e1080.jpg" >}}

至此，项目的配置文件准备完毕。

## 安装

接下来以群晖演示部署MIGPT。 🔻 首先准备好 docker-compose.yml 文件。`/volume1/test/miGPT/`要修改为配置文件夹的路径。

```yaml
version: '3.8'

services:
  mi-gpt:
    image: idootop/mi-gpt:latest
    container_name: mi-gpt-container
    env_file:
      - /volume1/test/miGPT/env
    volumes:
      - /volume1/test/miGPT/migpt.js:/app/.migpt.js
```

 🔻 再把 docker-compose 上传到配置文件的同级目录。

{{< figure src="./66b43c670c32d3250.png_e1080.jpg" >}}

🔻 打开群晖 Container Manager，新增项目，选择刚刚创建好的docker-compose文件。

{{< figure src="./66b43c69884f73406.png_e1080.jpg" >}}

🔻 启动项目。

{{< figure src="./66b43c69e49973406.png_e1080.jpg" >}}

🔻 日志没有报错就代表配置全部正确。

{{< figure src="./66b43c670b0a83250.png_e1080.jpg" >}}

## 使用

后面我们就可以利用配置文件中的唤醒词调用大语言模型了，同时也可以在配置文件中对大模型的角色进行配置。

{{< figure src="./66b43c69344073406.png_e1080.jpg" >}}

## 后记

有些特定型号的小爱音箱是不支持连续对话的，需要把`streamResponse`设置为false。

{{< figure src="./66b43c68f9e0c5517.png_e1080.jpg" >}}



通过调用[小米](https://pinpai.smzdm.com/1933/) IoT 生态开放接口的方案，无法完美实现在 AI 回复时让原来的小爱闭嘴。在唤醒模式下 `MiGPT` 会通过播放静音音频等方式让小爱闭嘴，达到“曲线救国”的目的。


