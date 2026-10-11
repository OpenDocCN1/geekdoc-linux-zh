
![](img/63f12be029370b8891d876ebe7b9f412_259_3.png)
![](img/63f12be029370b8891d876ebe7b9f412_259_4.png)
![](img/63f12be029370b8891d876ebe7b9f412_259_5.png)
![](img/63f12be029370b8891d876ebe7b9f412_259_6.png)
![](img/63f12be029370b8891d876ebe7b9f412_259_7.png)
![](img/63f12be029370b8891d876ebe7b9f412_259_8.png)
![](img/63f12be029370b8891d876ebe7b9f412_260_0.png)
![](img/63f12be029370b8891d876ebe7b9f412_260_1.png)
![](img/63f12be029370b8891d876ebe7b9f412_260_2.png)
![](img/63f12be029370b8891d876ebe7b9f412_260_3.png)
![](img/63f12be029370b8891d876ebe7b9f412_260_4.png)
![](img/63f12be029370b8891d876ebe7b9f412_260_5.png)
![](img/63f12be029370b8891d876ebe7b9f412_260_6.png)
![](img/63f12be029370b8891d876ebe7b9f412_260_7.png)
![](img/63f12be029370b8891d876ebe7b9f412_260_8.png)
![](img/63f12be029370b8891d876ebe7b9f412_260_9.png)
![](img/63f12be029370b8891d876ebe7b9f412_260_10.png)
![](img/63f12be029370b8891d876ebe7b9f412_260_11.png)

## Debian 12 安装设置

1. 按照 Debian 安装程序的提示操作：
   - 语言（Language）：选择您偏好的语言。
   - 位置（Location）：设置您的国家。
   - 键盘（Keyboard）：选择您偏好的布局。
   - 主机名（Hostname）：将主机名设置为 `freepbx`。
2. 域名（Domain Name）：
   - 您可以留空。
3. 设置 Root 密码（Root Password）：
   - 选择一个安全的密码并确认。
4. 创建新用户：
   - 添加用户。我为添加了一个名为 `louis` 的用户。
5. 分区（Partitioning）：
   - 选择“引导 - 使用整个磁盘并设置 LVM”（Guided - use entire disk and set up LVM）。
   - **不要使用加密** - 请记住，此镜像所在的主机系统已经使用了加密磁盘！
   - 选择磁盘并继续。
   - 确认更改以写入分区。
   - 磁盘设备通常可能是 `/dev/vda`。

## 1.9 安装后配置测试

重启后，以 `root` 身份登录。

## 2: 准备 Debian 12 安装

1. 重启后，以 `root` 身份登录。
2. 输入 `virsh dominfo freepbx` 检查此设置是否正确。
3. 如果你不执行此操作，一旦你重启了服务器（出于某种原因）并离开了家，就会发现为时已晚，你的电话系统失效了。
4.1 确保网络设置设置已设置为桥接模式以实现正确的网络集成。
2. 1.11
...
.......
.... 重启重启网络：
```bash
systemctl restart systemd-network
```
6. 输入 `ip addr` 查看您的 IP 地址是否有变化：
   - 静态 IP：
   - 您的网关：
   - DNS 服务器：

## 2.2 对 Debian 进行维护

- 更新软件包列表
- 升级所有软件包
- 移除不需要的软件包：
```bash
sudo apt update
sudo apt upgrade -y
sudo apt autoremove
```

## 2.3 下载并运行 FreePBX

- 检查 FreePBX 最新版本 (https://github.com/FreePBX/FreePBX-distro-debian)
- 使用 `wget` 下载脚本：
```bash
wget https://github.com/FreePBX/FreePBX-distro-debian/raw/master/install -o /tmp/install.sh
```
- 给脚本可执行权限：
```bash
chmod +x /tmp/install.sh
```
- 运行脚本：
```bash
sudo /tmp/install.sh
```
- 脚本完成后，安装 Asterisk、Apache 和 PHP：
```bash
sudo apt install asterisk apache2 php-mysql -y
```

## 3: 访问 FreePBX 界面

- 打开浏览器并访问 IP：http://192.168.1.60
- 按照向导配置您的设置。

## PBX 的优势

- 拥有自己的 PBX 意味着不再需要按用户付费。
- 我们根据主线使用情况付费，而不是用户数量。
- 通过 SIP 中继，他们不知道具体发生了什么，因此不会按分机或功能收费。
- 这就像是电话的 VPN ——他们不知道您有多少个分机，也不知道是否在录音通话。

## 业务电话系统设置

- 使用虚拟号码和可扩展的电话系统轻松处理您的业务。

## PBX 的好处是我们不按用户付费

## 1-855-YOURBIZ

- 轻松设置电话号码，可以随时随地添加、删除和扩展您的业务。

## 通过专业表现给客户留下印象

- 在您的营业时间内留下良好印象。然后让专业语音接听电话。

## 欢迎来到 UnitTel 仪表板

通过您的 UnitTel 客户门户，您可以管理您的账户。

## 总号码数

4

## 已绑定号码

0

首次使用 UnitTel SIP？

- 入门指南
- 配置 Grandstream UCM 指南
- 常见问题解答 (FAQ)

## 3.2 设置端点（入站呼叫的发送地）

当拨打 Unitel 的某个号码时，端点就是呼叫到达的地方。当你在 Unitel 中提供电话号码时，它会询问你将该号码的入站呼叫发送到哪里我们将先设置端点，这样当我们创建号码时，就已经有一个可以发送到的端点了。

导航到“Endpoints”（端点）部分

1. 从主仪表板，进入“Settings”（设置）
2. 点击“Endpoints”
3. 创建新端点（Create New Endpoint）
4. 点击“Add Endpoint”（添加端点）：
   5. 填写以下详情：
    * **Endpoint Description（端点描述）：输入一个描述端点的名称（例如：closet pbx）。
    * **Endpoint Destination（端点目的地）：插入你在在本指南之前的 FreeDNS Dynamic DNS 部分设置的动态 DNS 条目（例如：louishomeserver.chickenkiller.com）。这将解析到你 PBX 的外部 IP 地址。当特定号码接到入站呼叫时，它将呼叫发送到此 IP 上的 PBX。
   6. 点击“Add Endpoint”完成设置。

## 获取并配置电话号码

1. 导航到“Numbers”（号码）部分
   - 从仪表板，点击“Numbers”后，点击“Add Number”（添加号码）。
   - 购买一个号码。
2. 将购买的号码分配给端点
购买后，进入“Manage Numbers”（管理号码）。
* 找到购买的号码，点击“Actions”（操作）下的下拉菜单并点击“Number Mode”（号码模式）。
* 选择“Forward to Endpoint”（转发到端点）：选择你之前创建的端点（例如：closet pbx）。
* 点击 Update（更新）。

## 3.4 在 Unitel 中添加中继 (Trunk)

SIP 中继的作用：

SIP 中继是你连接到世界的媒介，展示了你的电缆媒体和频谱或 Verizon 如何将你连接到互联网的其他部分。*trunk*（中继）是你的电话系统 (PBX) 与外部电话之间的连接。它允许你的系统向外部世界拨打和接收电话。在 Unitel 中设置中继是必要的。

中继的目的是为你的 PBX 提供一条路径，使其能够在公共电话网络之间路由呼叫。如果没有正确配置的中继，你的系统将无法与外部电话号码通信。这就是我在编写本指南的三个周里一直在做的。

1. 登录 Unitel 管理界面
* 打开你的浏览器并进入 Unitel 管理界面。
