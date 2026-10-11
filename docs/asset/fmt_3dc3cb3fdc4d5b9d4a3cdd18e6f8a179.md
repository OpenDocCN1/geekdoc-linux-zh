
## head [options] file

`head` 在屏幕上显示文本文件的前 10 行。

- `-n lines`
  输出指定行数的行。

- `-n lines`
  返回除最后几行之外的所有文件。因此，`head -n 3` 返回除最后三行的所有文本。

## Alternatives

`tail` 实现相反的功能。例如，`tail -n 5` 返回文件的最后五行。如果你想跳过前五行，可以使用 `tail -n +6`（返回从第六行开始的所有行）。

## help name

`help` 显示指定 bash 命令的简短描述。`help` 适用于集成到 bash 中的命令，如 `alias`、`cd` 或 `type`。

## history [options] [n]

bash 命令历史记录按连续数字显示最近执行的命令。`n` 参数将输出限制为最后运行的命令。通过 `!n`，你可以重复指定数字的命令：`!-1`、`!-2` 等分别运行最后一次命令、倒数第二一次命令，以此此类推。

- `-c`
  删除内存中存储的命令序列（保留 `.bash_history`）。

- `-r [filename]`
  将存储在指定文件或 `.bash_history` 中的命令加载到历史内存中。

- `-w [filename]`
  保存命令序列（默认在 .bash_history 中）。

## host [options] name/ip-address

`host` 返回指定网络名称的 IP 地址或指定 IP 地址的网络名称。在许多发行版中，`host` 是 bind 软件包的组件，例如 `bind-utils` 或 `bind9-host`。

- `-a`
  提供额外的信息，可能帮助发现名称服务器配置中的错误。

- `-t type`
  返回所需类型的 DNS 条目。

## Example

IP 地址 `5.9.22.29` 和 `24a1:4f8:161:107::4` 分配给主机名 `kofler.info`。邮件服务器的域名为 `mail.kofler.info`。邮件服务器的 SPF 信息可以在 DNS 文本记录中找到。

```
$ host kofler.info
5.9.22.29 24a1:4f8:161:107::4

$ host mail.kofler.info
mail.kofler.info
```

## hostname [options]

`hostname` 返回当前主机名或设置主机名。

## hostnamectl [options] [command]

`hostnamectl` 命令提供有关主机名的信息并允许你更改它。

## htop

同名软件包中的 `htop` 是 `top` 的变体。相比 `top`，主要优势是你可以使用光标水平和垂直滚动进程列表。按 `K` 可以轻松结束选中的进程。

```
user$ htop
```

clock。

该命令还支持许多特殊函数，这些函数在 `man hwclock` 中有描述。

```
hydra [options] [hostname/ipaddress] service
```

同名软件包中的 `hydra` 破解或渗透测试命令从文件中读取密码或自行生成密码，并尝试使用它们登录网络服务。

`hydra` 支持广泛的服务，包括 FTP, HTTP(S), IMAP, MySQL, Microsoft SQL, POP3, PostgreSQL, SMTP, Telnet 和 VNC。该命令还可以尝试在 Web 表单（GET, PUT, POST）中进行登录。你可以使用 `hydra -h` 来确定允许的服务名称列表。

- `-V6`
  如果可能，使用 IPv6。

- `-C filename`
  使用文件中指定的用户名和密码组合。登录名和密码必须以 `login:password` 的格式逐行包含在文件中。

- `-e nsr`
  还会尝试空密码（n 代表 null）、将用户名作为密码（s 代表 same）以及反转用户名（r 代表 reverse）。

- `-f`
  一旦找到有效的登录名/密码组合，立即终止命令。

- `-l login`
  使用指定的用户名。

- `-L user file`
  从指定的文本文件中逐行读取用户名。

- `-m options`
  传递特定网络服务的额外选项。你可以使用 `hydra -U service` 来确定允许的选项，例如 `hydra -U http-get` 用于本应通过 HTTP GET 请求完成的登录。

- `-M host file`
  从文件中读取要攻击的主机名或 IP 地址，并并行攻击所有主机。

- `-o result file`
  将成功的密码组合保存到指定文件中，而不是显示在标准输出中。

- `-p password`
  使用指定的密码。

- `-P pwfile`
  逐一尝试指定文本文件中的密码。

- `-R`
  恢复上次通过 Ctrl+C 中断的 hydra 调用，前提是 `hydra.restore` 文件存在。不需要再指定其他选项；它们已包含在 `hydra.restore` 中。

- `-s portnr`
  使用指定的端口，而不是相应服务的默认端口。

- `-t n`
  并行运行 n 个任务（线程）。默认设置为 16。这可能太高了，因为某些服务如果有太多的并行请求（且来自同一个 IP 地址），将会阻塞登录。

- `-x min:max:chars`
  生成长度在 min 和 max 之间且包含指定字符的密码。这里，`a` 是小写字母的简写，`A` 代表大写字母，1 代表数字。所有其他字符（包括 äöß）必须单独输入。

示例：使用 `-x '4:6:aAl-$$'`，hydra 使用长度为 6 位且除字母和数字外包含字符 `-`, `_`, `$` 的密码。使用 `-x '4:4:1'`，hydra 会尝试所有四位数字。这将产生 10,000 种可能性。

`-x` 选项仅在特殊情况下有用，即你有（几乎）无限的时间，且目标计算机容忍无限次的登录尝试。

## 示例

在以下示例中，hydra 尝试在 Linux 服务器上寻找一个具有简单密码或无密码的 SSH 登录账户。为了实现这一点，首先使用 `cut` 生成所有账户的列表。理想情况下，你应该在运行与目标计算机相同发行版的计算机上运行此命令。

```
user$ cut -d: -f1 /etc/passwd > logins.txt
```

之后，hydra 应该尝试对存储在 `logins.txt` 中的所有账户进行 SSH 登录，使用用户名、反转后的用户名和空字符串作为密码：

```
user$ hydra -L logins.txt -t 4 -e nsr 10.0.0.36 targetthost
```

## 替代方案

如果你知道哈希值形式的密码，可以使用离线密码破解器（见 `john`）查找明文密码，`hashcat` 更快。但是此命令需要安装复杂的 GPU 驱动程序。

## iconv

`iconv -f charset1 -t charset2 in.txt > out.txt`

`iconv` 将字符集 1 转换为字符集 2。`iconv --list` 提供所有支持字符集的列表。以下命令从 Latin-1 编码的文件创建一个对应的 UTF-8 文件：

```bash
users iconv -f latin1 -t utf8 latin1dat > utf8dat
```

## id

`id` 指定用户的 ID、主组以及其他分配的组。在 Fedora 和 RHEL 上，该命令还会提供 SELinux 上下。

## 示例

用户 `kofler` 的 UID 为 1000，属于主组 `kofler`（GID 为 1000），并且是 `wheel` 组（GID 为 10）的成员：

```bash
root# id
uid=1000(kofler) gid=1000(kofler) groups=1000(kofler),10(wheel)
context=unconfined:u:unconfined r:unconfined_t:s0-s0:c0.c102
```

```bash
if condition; then
  commands
elif condition; then
  commands
else
  commands
fi
```

```
ifconfig [options] [interface]
```

```
ifup interface
ifdown interface
```
