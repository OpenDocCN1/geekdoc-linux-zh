

## 加固 Sendmail 服务器

在选择值之前，请研究你系统的实际使用模式，然后将该值设置为比观察到的最大值至少高出 50%，，以允许使用峰值。

`confCONNECTION_RATE_THROTTLE` 在与 `confMAX_DAEMON_CHILDREN` 完全相同的系统上非常有用。事实上，这两者经常一起使用。`confMAX_DAEMON_CHILDREN` 设置了并发邮件连接数量的绝对上限，而 `confCONNECTION_RATE_THROTTLE` 设置了爬升到该最大值的速率。攻击者可以轻易超过你设置的连接速率，从而拒绝你的访问。然而，设置速率可以保护你系统上的其他部分，以便你有一个可以运行的系统来处理攻击。

`confMAX_MESSAGE_SIZE` 定义了服务器接受的最大消息大小。任何大于此限制的消息都会被拒绝。默认情况下，Sendmail 接受任何大小的邮件。以下命令将覆盖并设置最大消息大小为 2,000,000 字节。

```
define(`confMAX_MESSAGE_SIZE`, `2000000`)
```

某些 DoS 攻击旨在通过向邮件队列暂留目录写入大型邮件来淹没文件系统。此参数旨在防御此类攻击，但很大程度上是无效的，因为攻击者可以改为发送大量较小的邮件来达到相同的效果。

完全保护 Sendmail 免受拒绝服务攻击是不可能的。上述描述的参数的真实目的是限制攻击造成的损害。同样，用于保护 Sendmail 免受未经授权访问的技巧，实际上也是为了保护整个系统。

## 保护 Sendmail 免受未经授权的访问

最危险的安全漏洞是那些利用未经授权的访问来获取 root 权限的。一旦入侵者获得了 root 权限，无法采取任何措施来保护系统上的任何内容，包括 Sendmail。大多数 Sendmail 安全措施的目的是确保 Sendmail 不被入侵者获取未经未经访问或 root 权限的手段。为此， Sendmail 依赖的用户 ID 和文件必须经过安全保护。

![](img/9639113aa446fb8976cb3d377f7aafdd_360_0.png)

 Sendmail 根据其执行的操作使用三个用户 ID。这三个用户 ID 是：

DefaultUser：这是 `sendmail.cf` 文件中的一个选项，用于标识运行邮件器和其他外部命令的用户 ID 和组 ID。`DefaultUser` 选项有三个默认值：

- 1. 如果在 `/etc/passwd` 文件定义了用户 `mailnull`，则使用分配给 `mailnull` 的用户 ID 和组 ID。
- 2. 如果 `/etc/passwd` 中未定义 `mailnull` 但定义了用户 `daemon`，则使用分配给 `daemon` 的用户 ID 和组 ID。
- 3. 如果 `/etc/passwd` 中未定义 `mailnull` 或 `daemon`，则使用 1 作为用户 ID，组 ID。

`DefaultUser` 选项的默认值可以通过在 m4 宏配置文件中使用 `CONF_USER` 参数为该选项定义特定值来覆盖。Red Hat 7 随附的宏配置文件包含以下 `CONF_USER_ID` 命令：

```
define('CONF_USER_ID', '8:12')
```

该命令将用户 ID 设置为 8，组 ID 设置为 12。这些值是与 Red Hat 7 提供的 `/etc/passwd` 文件中的用户名 `mailnull` 关联的。值得注意的是，Red Hat 7 的 `/etc/passwd` 文件中也有用户 `mailnull` 和用户 `daemon` 的条目，这并不意外，因为它们被多个不同的守护进程使用。另一方面，`mailnull` 必须被特意添加为 `DefaultUser` 选项的默认值，因为它没有其他用途。鉴于，这并不是 Red Hat 也为 `CONF_USER_ID` 参数定义值的原因。以下是 Red Hat 7 `/etc/passwd` 文件和 `/etc/shadow` 文件中的 `mail` 和 `mailnull` 条目：

```
[craig]$ grep mail /etc/passwd
mail:x:8:12:/var/spool/mail:
mailnull:x:47:47:/var/spool/mqueue:/dev/null
[root]# grep mail /etc/shadow
mail::*:11267:0:99999:7::
mailnull::*:11267:0:99999:7::
```

虽然 Red Hat 两个专门定义用于 `DefaultUser` 选项的 `/etc/passwd` 条目，但许多 Linux 系统并不提供此类条目。Red Hat 的两个示例显示了如果你添加 `mailnull` 账户时需要注意的两个特征。

# 加固 Sendmail 服务器 339

`mailnull` 不能有关联的密码，且不能有有效的登录 shell。在示例中，`mailnull` 在 `/etc/passwd` 文件中定义的登录 shell 为 `/dev/null`。此外，`mailnull` 用户没有有效的密码。

TrustedUser：此选项定义了拥有 Sendmail 文件的用户，例如数据库文件。TrustedUser 选项默认为 root。可以通过在 m4 宏配置文件中使用 `confTRUSTED_USER` 定义值来覆盖默认值：

```
define(`confTRUSTED_USER`, `root`)
```

TrustedUser 在 `/etc/passwd` 文件或 `/etc/shadow` 文件中没有有效密码。因此，`mailnull` 用户账户满足前两个要求。`mailnull` 用户账户的要求是不能拥有任何文件。这些三个要求防止账户被利用以获取未经授权的访问。

AsUser：此选项定义了运行 Sendmail 的用户。默认情况下，此选项未定义。如果定义了此选项，Sendmail 将以特定用户的身份运行。RunAsUser 选项旨在供防火墙服务器使用。在防火墙服务器上，邮件被接收、处理，然后转发到没有账户的内部邮件服务器。对于大多数配置，你需要在 `/etc/passwd` 中定义 `mailnull`。`mailnull` 成为 `DefaultUser`，这为你提供了文件创建和命令执行之间的分离。一旦为 `DefaultUser` 定义了 `mailnull`，`TrustedUser` 几乎不需要定义。对于大多数系统，root 是绝大多数服务器正确的 RunAsUser。

## 文件和访问安全

使用正确的用户 ID 只是故事的一部分。Sendmail 还需要小心它读取和写入的文件。维护以下标准有助于避免问题：

- Sendmail 读取的文件不应具有组写权限。例如，如果 `relay-domains` 文件是全局可读的，系统上的任何人都可以授予他们喜欢的垃圾邮件发送者转发权限。建议 Sendmail 读取的文件权限为 644。
- Sendmail 读取的文件应放在组写或可写目录中。再次，组中的任何人或系统上的任何人都可以创建 Sendmail 文件。建议 Sendmail 使用的目录权限为 755。
- Sendmail 读取或写入的文件不应是符号链接。

在某些情况下——例如读取 `.forward` 文件——Sendmail 会检查这些标准是否得到了维护。你可以通过在 m 配置文件中使用 `confDONTBLAME_SENDMAIL` 参数设置 `DontBlameSendmail` 选项来禁用 Sendmail 执行的文件访问检查。所有的 DontBlameSendmail都会降低安全性，因此此处不介绍。有关此选项的更多信息，请参附录 C，“Sendmail 变量、选项和标志”。

 Sendmail 对 `.forward` 文件非常小心，因为该文件可能包含一个通过 l 语言将邮件转发到程序的邮件地址，其中程序是要执行的程序名称。别名数据库也可以使用这种语法。

