# 在Linux上安装Warp





### 在Linux上安装Warp

官网安装说明：

[pkg.cloudflareclient.com](https://pkg.cloudflareclient.com/)

官网使用手册：

[Linux desktop client · Cloudflare WARP client docs](https://developers.cloudflare.com/warp-client/get-started/linux/)

**Ubuntu**：

```bash
# Add cloudflare gpg key
curl -fsSL https://pkg.cloudflareclient.com/pubkey.gpg | sudo gpg --yes --dearmor --output /usr/share/keyrings/cloudflare-warp-archive-keyring.gpg

# Add this repo to your apt repositories
echo "deb [signed-by=/usr/share/keyrings/cloudflare-warp-archive-keyring.gpg] https://pkg.cloudflareclient.com/ $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/cloudflare-client.list

# Install
sudo apt-get update && sudo apt-get install cloudflare-warp
```

**Debian**：

```bash
# Add cloudflare gpg key
curl -fsSL https://pkg.cloudflareclient.com/pubkey.gpg | sudo gpg --yes --dearmor --output /usr/share/keyrings/cloudflare-warp-archive-keyring.gpg

# Add this repo to your apt repositories
echo "deb [signed-by=/usr/share/keyrings/cloudflare-warp-archive-keyring.gpg] https://pkg.cloudflareclient.com/ $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/cloudflare-client.list

# Install
sudo apt-get update && sudo apt-get install cloudflare-warp
```

**Red Hat Enterprise Linux & CentOS**：

```bash
# Add cloudflare-warp.repo to /etc/yum.repos.d/
curl -fsSl https://pkg.cloudflareclient.com/cloudflare-warp-ascii.repo | sudo tee /etc/yum.repos.d/cloudflare-warp.repo

# Update repo
sudo yum update

# Install
sudo yum install cloudflare-warp
```





### 注册 WARP 客户端

```bash
sudo warp-cli register
```



### 检查 WARP 客户端状态

首先，使用 `warp-cli` 命令检查 WARP 客户端的连接状态：

```bash
sudo warp-cli status
```

输出应包含类似于以下内容的信息，表示 WARP 已连接：

```bash
Status update: Connected
```



### 检查 Warp+许可证

通过以下命令查看当前是否激活了Warp+许可证：

```bash
warp-cli account
```

如果显示的信息中包含您的Warp+许可证密钥或相关信息，则表明您正在使用Warp+。如果没有显示许可证信息，则说明您使用的是免费的Warp版本。



### 添加 Warp+许可证

如果您已经订阅了Warp+，可以通过以下命令激活Warp+功能：

```bash
sudo warp-cli set-license <LICENSE_KEY>
```

将 `<LICENSE_KEY>` 替换为您从Cloudflare获取的Warp+许可证密钥。



### 切换 WARP 的模式

1. **warp**:
   - 启用完整的 WARP 模式。
   - 使用 WireGuard 协议加密并路由所有流量，通过 Cloudflare 的网络提供隐私和性能提升。
2. **doh** (DNS over HTTPS):
   - 仅启用 DNS over HTTPS 功能。
   - 仅加密 DNS 查询，通过 HTTPS 协议将 DNS 查询发送到 Cloudflare 的 DNS 服务器，提升隐私和安全性。
   - 不影响其他网络流量，只处理 DNS 查询。
3. **warp+doh**:
   - 同时启用 WARP 和 DNS over HTTPS 功能。
   - 所有网络流量通过 WARP 隧道加密和路由，并且 DNS 查询通过 HTTPS 加密发送到 Cloudflare 的 DNS 服务器。
4. **dot** (DNS over TLS):
   - 仅启用 DNS over TLS 功能。
   - 仅加密 DNS 查询，通过 TLS 协议将 DNS 查询发送到 Cloudflare 的 DNS 服务器，提升隐私和安全性。
   - 不影响其他网络流量，只处理 DNS 查询。
5. **warp+dot**:
   - 同时启用 WARP 和 DNS over TLS 功能。
   - 所有网络流量通过 WARP 隧道加密和路由，并且 DNS 查询通过 TLS 加密发送到 Cloudflare 的 DNS 服务器。
6. **proxy**:
   - 启用代理模式。
   - 在这种模式下，流量通过 Cloudflare 的代理服务器传输，这样可以隐藏客户端的真实 IP 地址，提升隐私。
   - 具体实现和使用的协议可能依赖于 Cloudflare 的配置和实现。
7. **tunnel_only**:
   - 仅启用 WARP 隧道，不进行 DNS 查询的重定向。
   - 只加密和路由所有流量，不处理 DNS 查询，适合需要自定义 DNS 解析设置的用户。

**你可以使用以下命令切换模式：**

```bash
sudo warp-cli mode warp
sudo warp-cli mode doh
sudo warp-cli mode dot
sudo warp-cli mode warp+doh
sudo warp-cli mode warp+dot
sudo warp-cli mode proxy
sudo warp-cli mode tunnel_only
```

**选择适合的模式取决于你的需求：**

- **提高整体隐私和性能**：使用 `warp` 或 `warp+doh`。
- **仅保护 DNS 查询**：使用 `doh` 或 `dot`。
- **需要代理功能**：使用 `proxy`。
- **仅需要加密隧道，不影响 DNS**：使用 `tunnel_only`。



### 配置 WARP家庭模式

家庭模式可以帮助管理员限制设备上的访问，以确保儿童安全使用互联网。以下是这些命令的解释：

```bash
warp-cli dns families off
```

关闭家庭模式。这意味着关闭了所有的家庭过滤和限制，所有的网站都可以访问，没有任何限制。

```bash
warp-cli dns families malware
```

启用家庭模式并选择了恶意软件保护。在此模式下，Cloudflare WARP 将过滤掉已知的恶意软件网站，保护设备免受恶意软件的攻击。

```bash
warp-cli dns families full
```

启用家庭模式并选择了恶意软件保护和成人内容过滤。在此模式下，Cloudflare WARP 不仅会过滤掉已知的恶意软件网站，还会过滤掉包含成人内容的网站，以确保设备上的用户免受不良内容的影响。



### 连接/断开 WARP 

**连接**：
```bash
sudo warp-cli connect
```

**断开**：

```bash
sudo warp-cli disconnect
```



### 重启Warp服务

如果简单的断开和重新连接操作无法解决问题，可以尝试重启Warp服务：

使用以下命令重启Warp服务：

```bash
sudo systemctl restart warp-svc
```



### 解决ping google时ping不通，且显示ipv6地址

尝试禁用 IPv6 流量，以确保所有流量都通过 WARP 处理：

```bash
sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1
```



### 检查 IP 地址

使用在线服务检查您的外部 IP 地址。连接 WARP 后，您的 IP 地址应显示为 Cloudflare 分配的 IP 地址：

```bash
curl ifconfig.co
```

或

```bash
curl https://ipinfo.io/ip
```

您也可以使用以下命令，它将显示更多信息：

```bash
curl https://www.cloudflare.com/cdn-cgi/trace/
```

输出中应包含 `warp=on`，表示 WARP 已成功连接并在使用



### 检查 DNS 解析

确保 DNS 查询通过 Cloudflare 进行解析：

```bash
nslookup example.com
```

输出中应显示使用 Cloudflare 的 DNS 服务器（通常是 `1.1.1.1` 或 `1.0.0.1`）



### 检查 路由表

查看当前的路由表，确认 WARP 隧道已添加到路由表中：

```bash
ip route show
```

如果 WARP 正在运行，您应该能看到通过 WARP 隧道的路由条目



### Ping 测试

使用 ping 命令测试连接质量：

```bash
ping -c 4 1.1.1.1
```

如果能够成功 ping 通 Cloudflare 的 DNS 服务器，表明 WARP 连接正常



### 启用/关闭Linxu防火墙

**停止 `firewalld` 服务**:

```bash
sudo systemctl stop firewalld
```

**启动 `firewalld` 服务**:

```bash
sudo systemctl start firewalld
```

**禁用 `firewalld` 开机自启**:

```bash
sudo systemctl disable firewalld
```

**启用 `firewalld` 开机自启**:

```bash
sudo systemctl enable firewalld
```

**确认防火墙状态**:

```bash
sudo systemctl status firewalld
```



### 配置防火墙规则

在管理防火墙规则时，可以使用 `firewall-cmd` 命令。例如：

**确认防火墙状态**:

```bash
sudo firewall-cmd --state
```

**列出所有开放的端口**:

```bash
sudo firewall-cmd --list-ports
```

**开放一个端口（如80端口）**:

```bash
sudo firewall-cmd --permanent --add-port=80/tcp
或
sudo firewall-cmd --zone=public --add-port=80/tcp --permanent
sudo firewall-cmd --reload
```

**移除一个开放的端口（如80端口）**:

```bash
sudo firewall-cmd --permanent --remove-port=80/tcp
或
sudo firewall-cmd --zone=public --remove-port=80/tcp --permanent
sudo firewall-cmd --reload
```



### 查看当前使用的端口

**使用 `netstat`**

`netstat` 是一个网络统计工具，可以显示网络连接、路由表、接口统计信息、伪装连接以及多播成员。

```bash
sudo netstat -tuln
```

这条命令的含义：

- `-t`：显示 TCP 端口
- `-u`：显示 UDP 端口
- `-l`：显示监听的端口
- `-n`：以数字格式显示地址和端口号

**使用 `ss`**

`ss` 是另一个用来显示套接字统计信息的工具，功能类似于 `netstat`。

```bash
sudo ss -tuln
```

这条命令的含义与 `netstat -tuln` 类似。

**使用 `lsof`**

`lsof` 是一个列出打开文件的工具。由于在 UNIX 系统中，端口也是文件的一种，因此 `lsof` 也可以用来查看端口使用情况。

```bash
sudo lsof -i -P -n
```

这条命令的含义：

- `-i`：显示与网络相关的文件（即，端口）
- `-P`：显示端口号而不是服务名称
- `-n`：显示IP地址而不是主机名

**使用 `nmap`**

`nmap` 是一个网络扫描工具，可以用来扫描本地机器或远程机器上的开放端口。

```bash
sudo nmap -sT -O localhost
```

这条命令的含义：

- `-sT`：执行TCP连接扫描
- `-O`：尝试检测操作系统

**示例输出解释**

以下是使用 `ss -tuln` 命令的示例输出：

```less
State       Recv-Q      Send-Q           Local Address:Port           Peer Address:Port      
LISTEN      0           128                  0.0.0.0:22                0.0.0.0:*          
LISTEN      0           128                  0.0.0.0:80                0.0.0.0:*          
LISTEN      0           128                     [::]:22                   [::]:*          
LISTEN      0           128                     [::]:80                   [::]:*
```

在这个示例中：

- `0.0.0.0:22` 和 `[::]:22` 表示 SSH 服务在监听端口 22。
- `0.0.0.0:80` 和 `[::]:80` 表示 HTTP 服务在监听端口 80。
