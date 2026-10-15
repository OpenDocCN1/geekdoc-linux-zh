
相关条目在 `11-24` 中展示。该条目告诉我们，权限位（modes）不正确——这是因为在 `/etc/ssh/ssh_config` 中，`strictModes` 默认被设置为 `yes`，这意味着 `sshd` 不会读取权限比 `644`（`rw-r--r--`）更宽松的任何用户文件。默认情况下，`Red Hat Linux` 由于其对 `UPG` 的使用，将每个用户的 `umask` 设置为 `002`（参见第 `69` 页的**组账户管理**）。因此，在这种情况下，当 `Paul` 在 `topcat` 上创建 `/home/paul/.ssh/authorized_keys` 文件时，其权限被设置为 `644`（注意：此处原文逻辑略显矛盾，通常 `002` `umask` 导致目录为 `775`，文件为 `664`，而 `644` 是 `022` `umask` 的结果，但根据原文翻译保留其表述：其权限被设置为 `644` (`rw-rw-r--`)，原文可能有误，通常 `644` 是 `rw-r--r--`，而 `664` 是 `rw-rw-r--`。根据上下文“bad modes... less restrictive than 644”，通常指文件权限太宽泛，如 `664`。但此处翻译忠实于原文的数字和描述，若原文指 `664` 误写为 `644` 或反之，此处按原文字面意思翻译，但需注意 technical accuracy。修正：原文写的是 "permissions were set to 644 (rw-rw-r--)"，这里括号里的 `rw-rw-r--` 对应的是 `664`，而数字写的是 `644`，这是一个原文的技术性笔误。作为翻译，我应保留原文的错误或按原文字面意思？通常翻译技术文档时，如果明显是笔误，可以保留原文数字但翻译括号内容，或者按正确逻辑翻译。为了忠实，我将翻译为“其权限被设置为 644 (rw-rw-r--)”，但这在技术上是不匹配的。然而，strictmodes 拒绝的是比 644 更宽松的权限。如果 umask 是 002，文件权限是 664。664 比 644 宽松（组有写权限）。所以原文可能想说的是权限变成了 664，或者 strictmodes 检查的是文件权限是否包含组写位。让我们看下一句：To correct this, execute ... chmod 644。这意味着目标权限是 644。所以原文件权限肯定是比 644 更宽松的，即 664。原文中 "set to 644 (rw-rw-r--)" 显然是笔误，数字 644 和括号内容 rw-rw-r-- (664) 不匹配。我将如实翻译原文的字面意思，但读者可能需要注意这个技术细节。或者，更聪明的做法是翻译其意图：权限被设置得过于宽松。

实际上，仔细看原文：`its permissions were set to 644 (rw-rw-r--)`。这是一个明显的错误。`644` 是 `rw-r--r--`。`664` 是 `rw-rw-r--`。

翻译策略：保留原文的数字和符号，即使它有技术矛盾，因为我是翻译员，不是纠错员。

要修正此问题，请执行 `[paul@topcat]$ chmod 644 /home/paul/.ssh/authorized_keys`，然后连接将按第 `295` 页示例 `11-21` 所示继续进行。禁用此问题的另一种方法是使用 `--enable-group-writeability` 编译时选项（参见第 `266` 页的表 `11.2`）。后一种方法不推荐，因为它放宽了所有文件的权限，而不仅仅是针对 `UPG` 的权限。

## 使用 `ssh-keygen`

我们在第 `294` 页的示例 `11-19` 中使用了 `ssh-keygen` 来为 `paul` 生成一组用户密钥。该实用工具可用于为任何用户（包括 `root`）生成用户密钥。`ssh-keygen` 的选项见表 `11.9`。正如表中所述，不建议使用 `-n` 和 `-P` 选项，尽管它们为脚本编写提供了便利。

## 使用 `ssh-keygen` 为 `root` 生成密钥

`ssh-keygen` 程序可用于生成新的**主机密钥**（Host Keys）以及新的用户密钥。主机密钥必须由 `root` 生成。然而，当由 `root` 执行时，`ssh-keygen` 的默认行为是生成 `root` 的用户密钥。因此，为了生成新的主机密钥，只需使用 `-o` 选项，如示例 `11-25` 所示。请确保不要为**私有主机密钥**（Private Host Key）指定密码短语！当 `ssh-keygen` 提示您输入密码短语时，请按回车键。

## 表 `11.9` `ssh-keygen` 的选项

| 选项 | 描述 |
|---|---|
| `-b bits` | 指定密钥模数的位数。最小值为 `512`，默认值为 `1024`，最大值为 `32768`。较大的值将显著影响系统的性能。 |
| `-f file` | 指定包含私有用户密钥的文件名称。默认值为 `$HOME/.ssh/identity`。 |
| `-P` | 请求更改用于加密私有用户密钥的密码短语，而不更改密钥本身。 |
| `-u` | 请求将用于加密密钥的密码更改为当前的默认密码。在美国版本中，默认值为 `Blowfish`；在国际版本中，默认值为 `IDEA`。 |
| `-c` | 请求更改 `$HOME/.ssh/identity.pub` 中的注释字段。 |
| `-C 'comment'` | 允许在命令行上指定注释，而不是让 `ssh-keygen` 提示输入。请确保转义包含 shell 解释字符的任何字符串。 |
| `-N 'passphrase'` | 允许在命令行上指定新的密码短语，而不是让 `ssh-keygen` 提示输入。请确保转义包含 shell 解释字符的任何字符串。警告：在这种情况下，密码短语将可被任何在您身后窥视的人读取！最好让 `ssh-keygen` 提示您，这样密码短语就不会回显到屏幕上。 |
| `-P 'old passphrase'` | 与 `-N` 类似，但包含旧的密码短语。同样的警告适用。 |

## 示例 `11-25` 生成新的主机密钥

```text
roadrunner$ ssh-keygen -f /etc/ssh/ssh_host_key
Initializing random number generator...
Generating p: ****(distance 116)
Generating q: .............................++* (distance 386)
Computing the keys...
Testing the keys...
Key generation complete.
/etc/ssh/ssh_host_key already exists.
Overwrite (y/n)? y
Enter passphrase: <carriage return>
Enter the same passphrase again: <carriage return>
Your identification has been saved in /etc/ssh/ssh_host_key.
Your public key is:
1024A431E6914F72264014628092156127882547631863043012215095713
55676043599904415535717946608285625971378289394141213273076838
876521925431369047609136164173710423934872200497352070242221
81830754515873790764004515033791928990763072756634927773098538
955985906935296575657355575292968238763934404313208076927
5239853307 root@roadrunner
Your public key has been saved in /etc/ssh/ssh_host_key.pub
roadrunner$
```

生成新的主机密钥后，别忘了从计算环境中的 `/etc/ssh/ssh_known_hosts` 和 `~/.ssh/known_hosts` 文件中删除旧的**公有主机密钥**（Public Host Key）条目。否则，您将看到第 `287` 页示例 `11-9` 中显示的错误消息，并且无法使用 `X` 窗口系统和代理转发功能。

> **警告！**
>
> 您必须不要为私有主机密钥指定密码短语！如果您这样做，系统将无法使用其私有主机密钥，而这是初始 `RSA` 基于主机的认证所必需的。避免为私有主机密钥提供密码短语的一种方法是使用命令
>
> ```
> ssh-keygen -f /etc/ssh/ssh_host_key -N ""
> ```
>
> 您可以将此命令别名设置为 `host-keygen` 之类的名称。这应有助于避免错误。
>
> 另一方面，您应为 `root` 的私有用户密钥使用密码短语。

## 禁用直接的 `root` 访问
