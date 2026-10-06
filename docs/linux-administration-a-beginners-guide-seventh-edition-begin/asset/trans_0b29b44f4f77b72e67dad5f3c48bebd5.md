

# Linux 管理：入门指南

连接到 Asterisk 控制台并重新加载 SIP 配置：

```
server*CLI> sip reload
Reloading SIP
```

> 提示：你可以快速连接到正在运行的 Asterisk 进程并执行 Asterisk 命令，而无需始终连接到原生的 Asterisk 控制台。要此操作，你可以使用 `-rx` 选项，后跟跟你想要执行的子命令。

运行 `sip reload` 子命令的完整命令是：
# asterisk -rx "sip reload"
此外，要显示当前的拨号计划，你需要运行
# asterisk -rx "dialplan show"

在 Asterisk 控制台中，列出可用的 SIP 端点。你将在控制输出中看到你在 `sip.conf` 文件中配置的两个 SIP 电话。你会注意到 Host 为 ("Unspecified")（未指定），状态为 UNKNOWN（未知），表示设备离线状态。

```
server*CLI> sip peers
```

| Name/username | Host | Dyn | Forport | Comedia | ACL | Port | Status | Description |
|---|---|---|---|---|---|---|---|---|
| 1001 | (Unspecified) | D | Auto | (No) | No | 0 | UNKNOWN |
| 1002 | (Unspecified) | D | Auto | (No) | No | 0 | UNKNOWN |

2 sip peers [Monitored: 0 online, 2 offline unmonitored: 0 online, 0 offline]

# 拨号计划配置 (extensions.conf)

Asterisk 软件包随附的默认拨号计划存储在 `/etc/asterisk/extensions.conf` 文件。它在默认和未修改的状态下包含许多参数/设置；但由于这些练习不需要这些设置，我们将重命名或备份原始文件并从头创建一个新文件：

```
[root@server -]# mv /etc/asterisk/extensions.conf extensions.conf.original
```

之后，创建一个该文件的新空版本并修改其所有权和权限：

```
[root@server -]# touch /etc/asterisk/extensions.conf
[root@server -]# chown asterisk.asterisk /etc/asterisk/extensions.conf
[root@server -]# chmod 640 /etc/asterisk/extensions.conf
```

使用文本编辑器编辑新的 `/etc/asterisk/extensions.conf` 文件并添加以下内容：

```
[general]
;
[internal]
; 内部电话（分机）之间的拨号 - Alice 和 Bob
```

![](img/9f6657924397c33f088db5321b751a83_577_0.png)

## 下载并安装 X-Lite 手机软件
按照以下步骤在你想运行 SIP 客户端的每个客户端系统或设备上获取并配置 X-Lite 软件：

- 1. 启动你喜欢的浏览器并访问 www.counterpath.com/x-lite-download/。
- 2. 点击你要安装软电话的计算机对应的操作系统下载按钮。
- 3. 按照说明安装软件。
- 4. 启动 X-Lite 软件。
- 5. 在第二个运行 X-Lite 软件并作为第二个分机的系统上重复步骤 1–4。

![](img/9f6657924397c33f088db5321b751a83_578_0.png)

## 配置 SIP 分机
一旦你下载并安装了上述 SIP 客户端，就可以按照后续章节中的说明来测试你的基础 PBX。首先，我们将配置 SIP 分机。

- 1. 设置你的 SIP 账户。进入 首选项 (Preferences) -> 账户设置 (Account Settings)。

# 第 21 章 越网络协议 (VoIP)

- 2. 在下一个屏幕中填写以下值：
User ID: 1001
Domain: sip.server.com
Password: herSecret
Display name: Alice

![](img/9f6657924397c33f088db5321b751a83_579_0.png)

- 3. 点击 OK 将配置保存到 `sip.conf` 文件中并尝试连接到 Asterisk 服务器。你将看到以下屏幕：

![](img/9f6657924397c33f088db5321b751a83_579_1.png)

- 4. 当 SIP 客户端成功连接到服务器时，你可能会在 Asterisk 控制台中观察到如下：

```
server*CLI> -- Registered SIP '1001' at sip.server.com:5060
```

- 5. 重复之前的步骤 1-4 以配置第二个 X-Lite 客户端（Bob）。将 Alice 的信息（User ID: 1001, Password: herSecret, Display name: Alice）替换为 Bob 的正确信息（User ID: 1002, Password: hisSecret, Display name: Bob）。

在继续下一节之前，你可以在 Asterisk 服务器上运行以下命令来验证软件的配置并确保它们已注册：

```
server*CLI> sip peers
```

| Name/username | Host | Dyn | Forport | Comedia | ACL | Port | Status | Description |
|---|---|---|---|---|---|---|---|---|
| 1001 | 192.168.1.101 | D | Auto | (No) | No | 5060 | OK | |
| 1002 | 192.168.1.102 | D | Auto | (No) | No | 5060 | OK | |

