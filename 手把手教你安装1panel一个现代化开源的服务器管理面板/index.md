# 手把手教你安装1Panel,一个现代化开源的服务器管理面板


# 1.进入官网
[GitHub - 1Panel-dev/1Panel: 🔥 🔥 🔥 现代化、开源的 Linux 服务器运维管理面板。](https://github.com/1Panel-dev/1Panel)

# 2.一键安装
```
curl -sSL https://resource.fit2cloud.com/1panel/package/quick_start.sh -o quick_start.sh && sudo bash quick_start.sh
```

执行中,可以看到会自动安装docker-compose和docker

{{< image src="./4085218651.png" caption="图片1" >}}

安装完后访问即可,注意http协议:

{{< image src="./4043262894.png" caption="图片2" >}}


## 1 1pctl
1Panel 默认内置了命令行运维工具 1pctl，通过执行 1pctl help，可以查看相关的命令说明。

```
Usage:
  1pctl [COMMAND] [ARGS...]
  1pctl --help
 
Commands: 
  status              查看 1Panel 服务运行状态
  start               启动 1Panel 服务
  stop                停止 1Panel 服务
  restart             重启 1Panel 服务
  uninstall           卸载 1Panel 服务
  user-info           获取 1Panel 用户信息
  version             查看 1Panel 版本信息
  reset               重置 1Panel 系统信息

```

## 2 1pctl reset
重置 1Panel 系统信息，包括取消安全入口登录，取消两步验证等

```
Usage:
  1pctl reset [COMMAND] [ARGS...]
  1pctl reset --help
 
Commands: 
  domain              取消 1Panel 访问域名绑定
  entrance            取消 1Panel 安全入口
  https               取消 1Panel https 方式登录
  ips                 取消 1Panel 授权 IP 限制
  mfa                 取消 1Panel 两步验证

```
<br>

————————————————<br>
版权声明：本文为CSDN博主「生生世世是所说的」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_42901723/article/details/132641580

