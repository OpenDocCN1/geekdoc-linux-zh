
## Tripwire 入侵检测系统

Tripwire 是一个简单、有效的入侵检测系统（IDS）。它计算指定文件和目录的 MD5 校验和。这些校验和用于检测对文件系统进行的更改。未经授权的更改可能意味着发生了入侵。按照以下步骤设置 Tripwire：

### 安装 Tripwire

1. 以 `root` 身份登录并切换到 `/usr/local/src` 目录：
   ```bash
   cd /usr/local/src
   ```

2. 点击看起来像鼠标环绕着地球的图标启动 Mozilla。

3. 访问 `www.tripwire.org/downloads`。

4. 点击 `rpm4 - tripwire-2.3-47.i386.tar.gz` 链接。

5. 当“Downloading Tripwire-2.3-47.i386.tar.gz”窗口打开时，点击 OK 按钮。

6. 在打开的“保存文件名称”窗口中点击 Save 按钮，包含 Tripwire 的文件将保存到根目录。

7. 输入此命令提取 Tripwire RPM：
   ```bash
   tar xzf tripwire*
   ```
   `tar` 命令从你下载的文件提取 Tripwire RPM 包。

8. 安装 Tripwire 包：
   ```bash
   rpm -ivh tripwire*
   ```

现在你必须配置 Tripwire。Tripwire 围绕一个策略文件运行。策略文件告诉 Tripwire 需要检查哪些文件和目录以及检查什么。

### 配置 Tripwire 策略

1. 点击 GNOME 菜单按钮并选择 `Accessories::Text Editor`（文本编辑器）。打开 `/etc/tripwire/twpol.txt` 文件。

2. 保持文件中的前 166 行不变。删除此行之后的所有内容：
   - `# 在所有者和组方面应保持静态的常用访问目录`

3. 添加此 Tripwire 策略：

```
(
rule name = "system files"
severity = $(SIG_HI)
)

/etc -> $(SEC_CRIT) :
/sbin -> $(SEC_CRIT) :
/bin -> $(SEC_CRIT) :
/usr -> $(SEC_BIN) :
/usr/lib -> $(SEC_BIN) :
/lib

(
rulename = "optional and extra files, libraries, etc."
severity = $(SIG_MED)
)

/usr/local -> $(SEC_BIN) :
/opt -> $(SEC_BIN) :

(
rulename = "boot files"
severity = $(SIG_HI)
)

/boot
!/boot/System.map -> $(SEC_CRIT) :
!/boot/module-info :
```

此最小配置应被视为一个起点。随着你对 Red Hat Linux 计算机经验的增加，你应该修改这些文件。

4. 配置 Tripwire 本身。打开 GNOME Terminal 窗口并运行安装脚本：
   ```bash
   /etc/tripwire/twinstall.sh
   ```

5. 在提示时输入密钥文件短语（keyfile pass phrase）。该短语本质上是一个密码，用于加密 `/etc/tripwire/site.key` 文件，该文件本身用于加密校验和数据库。

6. 接下来，输入本地密钥文件短语。脚本会生成一个文件，其名称为你的限定域名并在末尾附加 `-local.key` 字符串。例如，如果你的计算机是 `cancun`，则文件名为 `cancun-local.key`。

系统会提示你输入在第 5 步中创建的站点短语（site key pass phrase）。Tripwire 使用站点短语加密 `twpol.txt` 文件并将其保存为 `tw.pol`。

7. 输入你的站点短语。

8. 在提示时输入本地短语。

在你输入短语后，策略数据文件将被签名。

9. 当 `twinstall.sh` 脚本完成后，初始化 Tripwire 校验和数据库。输入此命令：
   ```bash
   tripwire -init
   ```

10. 在提示时输入你的站点短语。

Tripwire 执行其工作。它为 `twpol.txt` 文件中列出的目录中的所有文件创建一个校验和数据库。Tripwire 配置为每天检查一次校验和数据库。默认情况下，它会将结果摘要通过邮件给 `root` 用户。你应该以 `root` 身份登录并定期检查摘要。

Tripwire 常在只读介质上创建未加密的数据库，以便成功的黑客可以掩盖踪迹。Tripwire 现在通过加密数据库让你的生活变得简单。除非你提供短语，否则黑客无法在你不知的情况下修改你的数据库。在本地媒体上维护 Tripwire 数据库可以节省时间和金钱。

### 测试 Tripwire

这些指令说明了如何更改文件并运行 Tripwire。Tripwire 会检测到更改，并由你决定该更改是否合法：

1. 更改重要系统文件的时间戳：
   ```bash
   touch /etc/hosts
   ```

2. 以检查模式运行 Tripwire：
   ```bash
   tripwire --check
   ```

3. Tripwire 计算 `/etc/hosts` 的校验和并与数据库中找到校验和进行比较。Tripwire 完成工作需要几分钟或更长时间。在 Tripwire 完成后，它会显示 `/etc/hosts` 发生了变化。在你收到文件已更改的通知后，确定更改是否有效或可能是由黑客引起的。传统上，Tripwire 存储在只读介质上以确保其不被篡改。例如，如果出现 IP 地址—`192.168.128.1`，你可以阻止它（该地址是虚构的）。输入此命令向你的 `iptables` 防火墙添加阻止规则：

## 第 16 章：保障您的未来 257
## 第四部分：呆者的复仇 256

Snort 是一个基于网络的入侵检测系统。它补充了 Tripwire。Snort 监控网络签名。你可以在 `www.snort.org` 找到更多信息。

## 下载 Snort
## 第四部分：呆者的复仇 258
