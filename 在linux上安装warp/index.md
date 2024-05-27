# 在Linux上安装Warp



## 一.在Linux上安装Warp/Warp+

如果您想在Linux上安装Warp或Warp+，可以按照以下步骤操作：

1. **安装必要的软件包**：

   ```bash
   sudo apt update
   sudo apt install curl
   ```

2. **下载并安装Warp客户端**：

   对于Warp免费版，您可以使用Cloudflare官方提供的安装脚本：

   ```bash
   curl https://pkg.cloudflareclient.com/install.sh | sudo bash
   ```

   或者您可以按照以下手动步骤进行安装：

   ```bash
   sudo apt install apt-transport-https
   
   curl -s https://pkg.cloudflareclient.com/pubkey.gpg | sudo gpg --dearmor -o /usr/share/keyrings/cloudflare-warp-archive-keyring.gpg
   
   echo "deb [signed-by=/usr/share/keyrings/cloudflare-warp-archive-keyring.gpg] https://pkg.cloudflareclient.com/ $(lsb_release -c -s) main" | sudo tee /etc/apt/sources.list.d/cloudflare-client.list
   
   sudo apt update
   
   sudo apt install cloudflare-warp
   ```

3. **启动Warp**：

   安装完成后，您可以启动Warp客户端：

   ```bash
   sudo warp-cli register
   sudo warp-cli connect
   ```

4. **升级到Warp+（可选）**：

   如果您已经订阅了Warp+，可以通过以下命令激活Warp+功能：

   ```bash
   sudo warp-cli set-license <LICENSE_KEY>
   sudo warp-cli connect
   ```

   将 `<LICENSE_KEY>` 替换为您从Cloudflare获取的Warp+许可证密钥。



## 二.查询您当前在Linux上使用的是Warp还是Warp+

1. **启动终端**：

   打开一个终端窗口。

2. **检查Warp状态**：

   使用以下命令检查Warp客户端的状态：

   ```bash
   warp-cli status
   ```
   
   该命令将显示Warp客户端的当前状态，包括连接状态和账户信息。

3. **检查Warp+许可证**：

   通过以下命令查看当前是否激活了Warp+许可证：

   ```bash
   warp-cli account
   ```
   
   如果显示的信息中包含您的Warp+许可证密钥或相关信息，则表明您正在使用Warp+。如果没有显示许可证信息，则说明您使用的是免费的Warp版本。

4. **示例输出**：

   运行 `warp-cli status` 命令后，您可能会看到类似以下的输出：

   ```sql
   Status update: Connected
   ```
   
   运行 `warp-cli account` 命令后，您可能会看到类似以下的输出：

   ```yaml
   Account type: Warp+ (license key: xxxxx-xxxxx-xxxxx-xxxxx)
   ```
   
   如果输出中显示 "Warp+" 和您的许可证密钥，则说明您正在使用Warp+。如果输出中只显示 "Warp" 而没有许可证密钥信息，则说明您使用的是免费版的Warp。
   
   

- 使用 `warp-cli status` 命令检查连接状态。
- 使用 `warp-cli account` 命令查看账户和许可证信息。



## 三.断开并重新连接

1. **断开当前连接**：

   使用以下命令断开Warp+的当前连接：

   ```bash
   sudo warp-cli disconnect
   ```

2. **重新连接**：

   使用以下命令重新连接Warp+：

   ```bash
   sudo warp-cli connect
   ```

3. **检查连接状态**：

   确认连接是否成功，可以使用以下命令检查Warp客户端的状态：

   ```bash
   warp-cli status
   ```

   该命令将显示当前的连接状态，确保显示 "Connected"。

   

## 四.重启Warp服务（如果上述方法无效）

如果简单的断开和重新连接操作无法解决问题，可以尝试重启Warp服务：

1. **重启Warp服务**：

   使用以下命令重启Warp服务：

   ```bash
   sudo systemctl restart warp-svc
   ```

2. **重新连接**：

   再次尝试连接Warp+：

   ```bash
   sudo warp-cli connect
   ```

3. **检查连接状态**：

   再次检查Warp客户端的状态：

   ```bash
   warp-cli status
   ```



- 使用 `sudo warp-cli disconnect` 断开连接。
- 使用 `sudo warp-cli connect` 重新连接。
- 使用 `warp-cli status` 检查连接状态。
- 如果问题持续，尝试使用 `sudo systemctl restart warp-svc` 重启Warp服务，然后再连接。



## 总结

- **Warp** 是一个免费的VPN服务，适合一般用户使用。
- **Warp+** 提供更高的速度和性能，适合需要更稳定和快速网络体验的用户。






