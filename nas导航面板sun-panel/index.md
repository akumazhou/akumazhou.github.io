# NAS导航面板Sun-Panel




**什么是 Sun-Panel ？**

> `Sun-Panel` 是一个服务器、`NAS` 导航面板、`Homepage`、浏览器首页。

{{< figure src="./ec52bbd5d3af12f65f418d5494f10927.png" >}}

**软件主要特点：**

- 🍉 界面简洁，功能强大，资源消耗低
- 🍊 简单易用，可视化操作，零代码使用
- 🍠 内外网模式一键切换
- 🍵支持 `Docker` 部署（兼容 `Arm` 系统）
- 🎪 支持多账户隔离
- 🎏 支持查看系统状态
- 🫙 支持自定义`JS`、`CSS`
- 🍻 使用简单，无需连接外部数据库
- 🍾 丰富的图标样式自由组合，支持[ Iconify 图标库](https://icon-sets.iconify.design/)
- 🚁 支持在网页中打开小窗口（部分第三方网站可能会屏蔽此功能）

官方提供了在线 `Demo`，地址：[http://sunpaneldemo.enianteam.com](http://sunpaneldemo.enianteam.com/)

## 安装

在群晖上以 Docker 方式安装。

在注册表中搜索 `sun-panel` ，选择第一个 `hslr/sun-panel`，版本选择 `latest`。

> 本文写作时， `latest` 版本对应为 `1.3.0`；

{{< figure src="./50f1b765db6592d422a7d0c585c42e44.png" >}}

### 卷

在 `docker` 文件夹中，创建一个新文件夹 `sun-panel`，并在其中建三个子文件夹 `conf`、`database` 和 `uploads`

| 文件夹                      | 装载路径        | 说明               |
| --------------------------- | --------------- | ------------------ |
| `docker/sun-panel/conf`     | `/app/conf`     | 存放设置文件       |
| `docker/sun-panel/uploads`  | `/app/uploads`  | 存放上传的图片文件 |
| `docker/sun-panel/database` | `/app/database` | 存放数据库         |

{{< figure src="./c73e7c196862e7c1704ee604eb858c01.png" >}}

### 端口

本地端口不冲突就行，不确定的话可以用命令查一下

```bash
# 查看端口占用
netstat -tunlp | grep 端口号
```

| 本地端口 | 容器端口 |
| -------- | -------- |
| `3004`   | `3002`   |

{{< figure src="./a04ea767e117392574d4af26d5babfa9.png" >}}

## 命令行安装

如果你熟悉命令行，可能用 `docker cli` 更快捷

```bash
# 新建文件夹 sun-panel 和 子目录
mkdir -p /volume1/docker/sun-panel/{conf,database,uploads}

# 进入 sun-panel 目录
cd /volume1/docker/sun-panel

# 运行容器
docker run -d \
   --restart unless-stopped \
   --name sun-panel \
   -p 3004:3002 \
   -v $(pwd)/conf:/app/conf \
   -v $(pwd)/uploads:/app/uploads \
   -v $(pwd)/database:/app/database \
   hslr/sun-panel:latest
```

也可以用 `docker-compose` 安装，将下面的内容保存为 `docker-compose.yml` 文件

```yaml
version: '3'

services:
  sun-panel:
    image: hslr/sun-panel:latest
    container_name: sun-panel
    restart: unless-stopped
    ports:
      - 3004:3002
    volumes:
      - ./conf:/app/conf
      - ./uploads:/app/uploads
      - ./database:/app/database
```

然后执行下面的命令

```bash
# 新建文件夹 sun-panel 和 子目录
mkdir -p /volume1/docker/sun-panel/{conf,database,uploads}

# 进入 sun-panel 目录
cd /volume1/docker/sun-panel

# 将 docker-compose.yml 放入当前目录

# 一键启动
docker-compose up -d
```

## 运行

在浏览器中输入 `http://群晖IP:3004` 就能看到登录界面

> 默认的账号：`admin@sun.cc` 和密码：`12345678`

{{< figure src="./0c48b4a74e3818619adbb2aff889b801.png" >}}

登录成功后的主界面

{{< figure src="./3b9667f42cdf9c1443252338c1e6f0ce.png" >}}

右下角进入 `设置` --> `账号管理`，可以编辑、修改、删除等操作，建议用自己的账号，并取消默认账号的权限

{{< figure src="./35b0303dcf9b372067aac139a79a8415.png" >}}

接下来进入 `分组管理`，创建自己的分组

{{< figure src="./bd39245ae9071d626ebea53b3673e154.png" >}}

现在可以开始添加导航了

{{< figure src="./6215e116c4f79dcd562f6c344d5a5b69.png" >}}

注意，这里有个 `地址` 和 `内网地址`，其中 `地址` 就是指的公网地址，`内网地址` 则指的是局域网地址，可以通过右下角的按钮进行切换

{{< figure src="./1e4e4f840cd3eabe7618ddc1e6a54b2c.png" >}}

当一个应用反代之后，可以让我们在不同的网络下使用不同的访问地址

{{< figure src="./8fb05fb7f0da38907bce5414a8975e1e.png" >}}

选择 `在线图标`，打开 `在线图标库`，搜索图标

{{< figure src="./7a3f212b34a217f94865a61ec38d0ccf.png" >}}

选中图标后，点图标复制

{{< figure src="./4697fcbed1dfaaae2e95211b49ad1097.png" >}}

回到 `Sun-Panel` 粘贴，没问题的话马上就能看到预览

{{< figure src="./56f08e9b4cc155b02f3681bcd6fb0633.png" >}}

像没有内网地址的可以不填

{{< figure src="./659734e9a7534aca2a8b917c5cefbbc7.png" >}}

大致的效果

{{< figure src="./8c382aea27f9b47c6c6198cc3ec47a29.png" >}}

## 参考文档

> hslr-s/sun-panel: A server, NAS navigation panel, Homepage, browser homepage. | 一个服务器、NAS导航面板、Homepage、浏览器首页。
> 地址：https://github.com/hslr-s/sun-panel

> Sun-Panel | Sun-Panel
> 地址：https://sun-panel-doc.enianteam.com/

> Open Source Icon Sets - Iconify
> 地址：https://icon-sets.iconify.design/

