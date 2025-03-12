# 小米音箱+DeepSeek让小爱秒变贾维斯




### 先简单介绍一下本次会用到的工具

一个专门将小爱接入AI的开源项目：**mi-gpt**

**地址：**https://github.com/idootop/mi-gpt

已经有**10.1k的 Star了**

{{< figure src="./650.png" >}}

流程也不是很复杂，大致如下：

```
1.配置im-gpt项目文件；

2.docker启动im-gpt；

3.如果要使用豆包音色，还需配置、启动imgpt-tts项目；

4.修改im-gpt相关配置，重新启动即可
```

在开始之前，先看看您的小爱音箱是否在如下所支持的型号内

型号一般在音箱底部可见

{{< figure src="./651.png" >}}

{{< figure src="./652.png" >}}

好了，介绍差不多了，我们开整~



### 小米音箱接入DeepSeek



本次使用docker一键启动mi-gpt项目（要确保本地电脑已经安装，并启动了**docker-desktop**）

所以我们其实并不需要下载mi-gpt的源码

只需要准备好它的配置文件即可

有两个配置文件：.**env和****.migpt.js**（随便放到某个文件夹下）

{{< figure src="./653.png" >}}

将这两个配置文件可以去github仓库中获取

{{< figure src="./654.png" >}}

也可公众号后台私信：“mi-gpt” 获取两个配置文件

其中**.env**文件是配置AI老三样的地方（**模型名称、apikey、api地址**），这里模型我选择deepseek-chat，也就是V3。

{{< figure src="./655.png" >}}

可以选择配置DeepSeek官方的API

也可以选择API中转站，比如**kg中转站**：https://kg-api.cloud/

*PS：选择中转站的好处就是后续想换模型，只需要改模型名称即可，非常方便。*

kg中转站的apikey在下图位置获取

{{< figure src="./656.png" >}}

api地址填：https://kg-api.cloud/v1

配置完成之后把.env文件保存



接下来我们看另外一个配置文件：**.migpt.js**

这个配置文件中，我们重点关注userId（小米id）、password（小米账号密码）、和did

{{< figure src="./657.png" >}}

即便用的不是小米手机也不用担心没有小米id

我们可以通过米家App获取上面的三个配置

首先去app商城下载一个**米家App**

{{< figure src="./658.png" >}}

在登录页面，用账号、密码登录（密码要记住，需要填写到配置中的password处）

*PS：即便没有账号，也可以点击注册，去注册一个*

{{< figure src="./659.png" >}}

登录之后，点击右下角 我的，下图红框中的数字，就是userId

{{< figure src="./660.png" >}}

进入米家首页，如下图，音箱的名称就是did（我的是 小爱音箱Pro）

*PS：音箱和电脑需要在同一局域网内（连同一个WiFi）*

{{< figure src="./661.png" >}}

MIot的配置，我的是小爱音箱Pro，默认配置跟表格里面指定配置一样，所以我的不用改

{{< figure src="./662.png" >}}

{{< figure src="./679.png" >}}

关于机器人角色，主人角色设定

下图的配置中bot代表机器人的信息，master代表你自己的信息

{{< figure src="./663.png" >}}

botProfile代表机器人的人设，masterProfile代表你自己的人设

systemTemplate是系统提示词，{{}}中的参数是变量名，程序启动之后会自动替换成指定的值。

{{< figure src="./664.png" >}}

下面的配置 注释得很清楚了，就不逐一介绍了。

{{< figure src="./665.png" >}}

另外如果您的小米机型不在如下行列，可以关闭streamResponse连续对话（设置为false）

{{< figure src="./680.png" >}}

我的是小爱音箱Pro，可开启（设置为true）

{{< figure src="./666.png" >}}

.migpt.js文件配置完毕之后记得保存

然后**win+r**，输入cmd 回车，进入windows控制台

输入如下指令：

```dockerfile
docker run -d --env-file $(pwd)/.env -v $(pwd)/.migpt.js:/app/.migpt.js idootop/mi-gpt:latest
```

注意⚠️：**$(pwd)**要换成相关配置文件所在的绝对路径

比如我的两个配置文件都在C:/Users/kangarooking/Documents/mi-gpt目录，那么**$(pwd)**就替换成这段路径即可

如下：

```dockerfile
docker run -d --env-file C:/Users/kangarooking/Documents/mi-gpt/.env -v C:/Users/kangarooking/Documents/mi-gpt/.migpt.js:/app/.migpt.js idootop/mi-gpt:latest
```

**特别注意：**大家在启动mi-gpt的时候千万不要开魔法，否则会判断异地登录，即便授权之后也要等1个小时才能再次用mi-gpt登录，我就是忘关了，，，

{{< figure src="./667.png" >}}

出现异地登录的问题，请使用相同的魔法地址，浏览器登录一下小米官网，重启im-gpt服务就ok啦 

执行之后如下

{{< figure src="./668.png" >}}

可以去docker-desktop中查看日志

{{< figure src="./669.png" >}}

{{< figure src="./681.png" >}}

到这里就大功告成啦~

后续修改配置，需要重启im-gpt服务才会生效。

问题和回复内容都会在日志里面显示

{{< figure src="./670.png" >}}

使用的时候还是要先说："小爱同学"，唤起小爱。

然后提问的关键词需要带如下图配置好的前缀，比如你要说："你在干嘛"，会唤起AI回复，如果你说："在干嘛"，是不会唤起AI回复的。

{{< figure src="./671.png" >}}

如果你嫌弃小米原生语音的话，可以配置切换成豆包的语音（有多种音色可选）。

这时候我们就需要用到火山引擎的TTS接口。



### TTS配置，火山引擎语音



首先，我们需要去火山引擎，进入「语音技术」页面

地址：https://console.volcengine.com/speech/app

创建应用，勾选「语音合成」

{{< figure src="./672.png" >}}

有20000次的用量赠送，够用好久了

{{< figure src="./673.png" >}}

创建应用之后，在语音合成这里找到appid和access token复制备用

{{< figure src="./674.png" >}}

这次我们需要另外启动一个服务：**migpt-tts**

随便找一个文件夹，创建一个**.env**文件，将如下内容复制到文件中

```yaml
# 基础配置# SECRET_PATH=你的接口访问秘密路径，比如：are-you-ok（可选）TTS_DEFAULT_SPEAKER=东北老铁# 火山引擎，官方文档：https://www.volcengine.com/docs/6561/79817VOLCANO_TTS_APP_ID=2xxxx57VOLCANO_TTS_ACCESS_TOKEN=wrI_xxxxxxxx_ADF#VOLCANO_TTS_USER_ID=火山引擎账号 ID（可选）# 微软必应 Read Aloud，官方文档：https://www.microsoft.com/zh-cn/edge/features/read-aloudEDGE_TTS_TRUSTED_TOKEN=你的必应 trust token，比如：6A5A-xxxx# OpenAI TTS，官方文档：https://platform.openai.com/docs/guides/text-to-speechOPENAI_API_KEY=你的 OpenAI API Key，比如：sk-proj-xxxxOPENAI_TTS_MODEL=tts-1OPENAI_BASE_URL=https://api.openai.com/v1
```

VOLCANO_TTS_APP_ID=填写语音合成的appid

VOLCANO_TTS_ACCESS_TOKEN=填写语音合成的access token

TTS_DEFAULT_SPEAKER=选择音色（写音色名称即可）

音色选择地址：

https://github.com/idootop/mi-gpt-tts/blob/main/src/tts/volcano.ts

{{< figure src="./682.png" >}}

配置完成之后保存

win+r，输入cmd 回车，进入windows控制台

输入如下指令：

```dockerfile
docker run -d --env-file ${pwd}/.env -p 3000:3000 idootop/mi-gpt-tts:latest
```

同样**${pwd}**需要替换成.env文件所在的绝对路径

启动之后日志如下，需要把接口地址记下来

{{< figure src="./675.png" >}}

**修改mi-gpt的****.migpt.js**配置文件，修改内容如下

把tts的值改为 **custom**

{{< figure src="./676.png" >}}

**修改mi-gpt的****.env**配置文件，修改内容如下

把**TTS_BASE_URL**的#号去掉，值改成migpt-tts的接口地址，但是域名不要写localhost，写你电脑的局域网ip地址

{{< figure src="./677.png" >}}

局域网ip可以在控制台通过**ipconfig**指令查看

{{< figure src="./678.png" >}}

保存后最好删除mi-gpt容器，重新执行指令启动。

然后就可以愉快的玩耍啦~

不过实测有个缺点：小爱会在AI回复之前抢答1~2秒，除了刷机，目前社区还没有很好的解决方案。

