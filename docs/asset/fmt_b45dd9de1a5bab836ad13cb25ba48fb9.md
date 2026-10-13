
`rulename` = "optional and extra files, libraries, etc."

`severity` = `$(SIG_MED)`

)

/usr/local -> `$(SEC_BIN)` :

/opt -> `$(SEC_BIN)` :

(

`rulename` = "boot files"

`severity` = `$(SIG_HI)`

)

/boot

!/boot/System.map -> `$(SEC_CRIT)` :

!/boot/module-info :

```
```
此最小配置应被视为一个起点。随着你对 Red Hat Linux 计算机经验的增加，你应该修改这些文件。

### 配置 Tripwire

- 4. 配置 Tripwire 本身。打开 GNOME Terminal 窗口并运行安装脚本：`/etc/tripwire/twinstall.sh`
- 5. 在提示时输入密钥文件短语（keyfile pass phrase）。该短语本质上是一个密码，用于加密 `/etc/tripwire/site.key` 文件，该文件本身用于加密校验和数据库。
- 6. 接下来，输入本地密钥文件短语。脚本会生成一个文件，其名称为你的限定域名并在末尾附加 `-local.key` 字符串。例如，如果你的计算机是 cancun，则文件名为 `cancun-local.key`。

系统会提示你输入在第 5 步中创建的站点短语（site key pass phrase）。Tripwire 使用站点短语加密 `twpol.txt` 文件并将其保存为 `tw.pol`。
- 7. 输入你的站点短语。
- 8. 在提示时输入本地短语。

在你输入短语后，策略数据文件将被签名。
- 9. 当 `twinstall.sh` 脚本完成后，初始化 Tripwire 校验和数据库。输入此命令：

```
tripwire -init
```
- 10. 在提示时输入你的站点短语。

Tripwire 执行其工作。它为 `twpol.txt` 文件中列出的目录中的所有文件创建一个校验和数据库。Tripwire 配置为每天检查一次校验和数据库。默认情况下，它会将结果摘要通过邮件给 root 用户。你应该以 root 身份登录并定期检查摘要。

Tripwire 常在只读介质上创建未加密的数据库，以便成功的黑客可以掩盖踪迹。Tripwire 现在通过加密数据库让你的生活变得简单。除非你提供短语，否则黑客无法在你不知的情况下修改你的数据库。在本地媒体上维护 Tripwire 数据库可以节省时间和金钱。

![](img/cc58a1e8691061866010ce216f881372_280_0.png)

测试 Tripwire。这些指令说明了如何更改文件并运行 Tripwire。Tripwire 会检测到更改，并由你决定该更改是否合法：
- 1. 更改重要系统文件的时间戳：

```
touch /etc/hosts
```
- 2. 以检查模式运行 Tripwire：

```
tripwire --check
```
- 3. Tripwire 计算 `/etc/hosts` 的校验和并与数据库中找到校验和进行比较。Tripwire 完成工作需要几分钟或更长时间。在 Tripwire 完成后，它会显示 `/etc/hosts` 发生了变化。在你收到文件已更改的通知后，确定更改是否有效或可能是由黑客引起的。传统上，Tripwire 存储在只读介质上以确保其不被篡改。例如，如果出现 IP 地址—192.168.128.1，你可以阻止它（该地址是虚构的）。输入此命令向你的 iptables 防火墙添加阻止规则：

# 第四部分：书呆族的复仇

```bash
iptables -A INPUT -s 192.168.128.1 -j DROP
```
