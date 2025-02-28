# OCRmyPDF让你能搜索扫描版PDF文档




# OCRmyPDF让你能搜索扫描版PDF文档



**什么是 OCRmyPDF ？**

> `PDF` 是存储和交换扫描文档的最佳格式。不幸的是，`PDF` 可能很难修改。`OCRmyPDF` 是一个 `Python` 应用程序和库，可以轻松地将图像处理和 `OCR`（可识别、可搜索的文本）应用于现有 `PDF`，通过向扫描的 `PDF` 文件添加 `OCR` 文本层，使你可以搜索或复制粘贴它们。

## 镜像下载

在群晖上以 Docker 方式安装。

在注册表中搜索 `ocrmypdf` ，选择第一个 `jbarlow83/ocrmypdf`，版本选择 `latest`。

> 本文写作时， `latest` 版本对应为 `v15.4.2`；

{{< figure src="./ab9d44ead8901e65eeecab4439b56696.png" >}}

你也可以使用命令行，用 `SSH` 客户端登录到群晖后，依次执行下面的命令

```bash
# 拉取镜像
docker pull jbarlow83/ocrmypdf:latest
```

如果拉不动，可以试试 `docker` 代理网站：https://dockerproxy.com/，但是会多几个步骤

```bash
# 如果拉不动的话加个代理
docker pull dockerproxy.com/jbarlow83/ocrmypdf:latest

# 重命名镜像（如果是通过代理下载的）
docker tag dockerproxy.com/jbarlow83/ocrmypdf:latest jbarlow83/ocrmypdf:latest

# 删除代理镜像（如果是通过代理下载的）
docker rmi dockerproxy.com/jbarlow83/ocrmypdf:latest
```

下载完成后，可以在 `映像` 中找到

{{< figure src="./d719a899a4c8cb10ac081480448833e9.png" >}}

## 准备工作

【说明】：

> 1. 与典型的 `Docker` 容器不同，`OCRmyPDF Docker` 容器是短暂的，它为一个 `OCR` 作业运行并终止，就像命令行程序一样。因此，我们通常使用 `--rm` 参数在容器退出时将其删除。
> 2. 默认情况下，`Docker` 镜像包括英语、德语、简体中文、法语、葡萄牙语和西班牙语，所以中文用户不需要添加语言包。

在 `docker` 文件夹中，创建一个新文件夹 `ocrmypdf`

```bash
# 新建文件夹 ocrmypdf 
mkdir -p /volume1/docker/ocrmypdf

# 进入 ocrmypdf 目录
cd /volume1/docker/ocrmypdf
```

准备一个文档用于测试，这是网页上打印生成的 `pdf` 文件，直接搜索 `sam` 是没有 `没有匹配项`

{{< figure src="./b5398119c32a4ab33f429abb25473af1.png" >}}

将这个文档放入 `ocrmypdf`，命名为 `input.pdf`

{{< figure src="./968e9971d3a1a3eb878abe005a00a33f.png" >}}

## 测试验证

为了方便起见，创建一个 `shell` 别名来隐藏 `Docker` 命令。通过使用 `alias` 命令，为长或复杂的命令创建简短且易记的别名，以便更快地执行常用操作或减少输入的工作量

```bash
# 创建别名
alias docker_ocrmypdf='docker run --rm  -i --user "$(id -u):$(id -g)" --workdir /data -v "$PWD:/data" jbarlow83/ocrmypdf:latest'

# 运行 OCR
docker_ocrmypdf /data/input.pdf /data/output.pdf
```

其中：

- `-- rm`：表示在容器退出时，会将其删除；
- `--user "$(id -u):$(id -g)"`：用于指定在容器内运行的用户和组，确保容器内的进程以与宿主机相同的用户权限运行，以防止权限问题；
- `--workdir /data`：指定容器内的工作目录；
- `-v "$PWD:/data"`：将 `/volume1/docker/ocrmypdf` 映射到了容器内的 `/data` ；

{{< figure src="./2116e7a488c689ea51aa59a32929ef01.png" >}}

运行完成后，会在 `ocrmypdf` 中看到多出了一个文件 `output.pdf`

{{< figure src="./abdc7f2f64eb48715f15bbe44c4816b2.png" >}}

下载到本地后，用 `pdf` 阅读器打开后，继续搜索 `sam` 显示有 `2` 处匹配

{{< figure src="./a7ae552d017000e32ac7a36c600c7e65.png" >}}

第二处

{{< figure src="./cc0fd7ea020e1a6eacf2a1d6b1daa0b5.png" >}}

`OCRmyPDF` 不仅提供了基本的 `OCR` 功能，还包括一些高级功能，如自动旋转、自动裁剪、去除文本阴影、增强图像质量等。它使用了一些优秀的开源工具和库，如 `Tesseract OCR` 引擎、`Ghostscript` 和 `ImageMagick`，以提供强大的 `OCR`和 `PDF`处理功能，当然，`OCRmyPDF` 无法打开使用数字证书加密的文档。

## 后续使用

```bash
# 登录群晖
ssh 用户名@IP

# 进入 ocrmypdf 目录
cd /volume1/docker/ocrmypdf

# 创建别名（运行docker_ocrmypdf后自动删除）
alias docker_ocrmypdf='docker run --rm  -i --user "$(id -u):$(id -g)" --workdir /data -v "$PWD:/data" jbarlow83/ocrmypdf:latest'

# 删除别名（建立后不想运行了）
unalias docker_ocrmypdf

# 运行 OCR
docker_ocrmypdf /data/input.pdf /data/output.pdf
```



## 参考文档

> ocrmypdf/OCRmyPDF: OCRmyPDF adds an OCR text layer to scanned PDF files, allowing them to be searched
> 地址：https://github.com/ocrmypdf/OCRmyPDF

> OCRmyPDF documentation
> 地址：[https://ocrmypdf.readthedocs.io](https://ocrmypdf.readthedocs.io/)

> jbarlow83/ocrmypdf - Docker Image | Docker Hub
> 地址：https://hub.docker.com/r/jbarlow83/ocrmypdf

