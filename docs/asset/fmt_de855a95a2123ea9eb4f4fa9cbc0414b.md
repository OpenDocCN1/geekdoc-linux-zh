
# 创建必要的 Maildir 目录

一旦 Exim 使用新的配置选项启动，我们必须在每个用户目录下创建 Maildir 目录，因为 Exim 不会自动为我们创建它。

## 第 1 步

默认情况下，邮件软件不会创建 Maildir 目录，我们必须在每个用户主目录下创建，以确保邮件传递无误。

- 创建 Maildir 目录，使用以下命令：
`[root@deep #] mkdir -p /home/sysadmin/Maildir`

在上面的示例中，我为用户“sysadmin”创建了新的 Maildir 目录。不要忘记对系统上的每个额外用户执行此操作，否则他们将无法接收邮件。

### 第 2 步

现在，将 Maildir 目录的权限设置为 `(0700/drwx------)`，并归拥有主目录的用户“sysadmin”所有。

- 可以以下命令完成：
`[root@deep #] chown sysadmin.sysadmin /home/sysadmin/Maildir`

# 带有邮件配额支持运行 Exim

本节仅适用于你想运行带有配额（quota）支持的 Exim。是的，Exim 对邮件配额有原生支持，这意味着通过此功能，你不再需要使用诸如“quota”之类的外部程序来为邮件用户提供配额支持，并可以使用 Exim 的配额能力来实现相同的功能。

在进入使用 Exim 启用邮件配额的步骤之前，重要的是，之前描述的 Maildir 格式应该已经在 Exim 中启用。这一点非常重要，因为邮件配额是在用户主目录下启用的，如果你不启用，它将无法工作。现在，让我们进入使用 Exim 启用邮件配额的步骤。

# 在 exim 配置中添加所需的 Maildir 参数

首先，我们必须在 `exim.conf` 文件中添加一些新选项，以便 Exim 配置为带有 Maildir 运行。我们必须小心与 Maildir 相关的额外配置行添加到 `exim.conf` 文件中的顺序。

## 第 1 步

为了让 Maildir 与 Exim 工作，我们必须更改 `exim.conf` 文件中“Transports Configuration”部分默认的“local_delivery”选项。

更改“Transports Configuration”部分中的行。粗体文本是默认 exim.conf 文件中更改的内容。

- 编辑 exim.conf 文件（`vi /etc/mail/exim.conf`）并更改以下行：

```
local_delivery:

driver = appendfile

file = /var/mail/$local_part

delivery_date_add

envelope_to_add

return_path_add

group = mail

mode = 0600
```

修改为：

```
local_delivery:

driver = appendfile

check_string = ""

create_directory

delivery_date_add

directory = ${home}/Maildir/

directory_mode = 700

envelope_to_add

group = mail

dir_format

message_prefix = ""

message_suffix = ""

mode = 0600

return_path_add
```

### 第 2 步

现在，我们必须重启 Exim 守护进程使更改生效。

- 重启 Exim，使用以下命令：

```
[root@deep ~]# /etc/init.d/exim restart

Shutting down Exim: [OK]

Starting Exim: [OK]
```

# 创建必要的 Maildir 目录

一旦 Exim 使用新的配置选项启动，我们必须在每个用户目录下创建 Maildir 目录，因为 Exim 不会自动为我们创建它。

## 第 1 步

默认情况下，邮件软件不会创建 Maildir 目录，我们必须在每个用户主目录下创建，以确保邮件传递无误。

- 创建 Maildir 目录，使用以下命令：
`[root@deep #] mkdir -p /home/sysadmin/Maildir`

在上面的示例中，我为用户“sysadmin”创建了新的 Maildir 目录。不要忘记对系统上的每个额外用户执行此操作，否则他们将无法接收邮件。

### 第 2 步

现在，将 Maildir 目录的权限设置为 `(0700/drwx------)`，并归拥有主目录的用户“sysadmin”所有。

- 可以以下命令完成：
`[root@deep #] chown sysadmin.sysadmin /home/sysadmin/Maildir`

# 带有邮件配额支持运行 Exim

本节仅适用于你想运行带有配额支持的 Exim。是的，Exim 对邮件配额有原生支持，这意味着通过此功能，你不再需要使用诸如“quota”之类的外部程序来为邮件用户提供配额支持，并可以使用 Exim 的配额能力来实现相同的功能。

在进入使用 Exim 启用邮件配额的步骤之前，重要的是，之前描述的 Maildir 格式应该已经在 Exim 中启用。这一点非常重要，因为邮件配额是在用户主目录下启用的，如果你不启用，它将无法工作。现在，让我们进入使用 Exim 启用邮件配额的步骤。

# 在 exim 配置中添加所需的 Maildir 参数

首先，我们必须在 `exim.conf` 文件中添加一些新选项，以便 Exim 配置为带有 Maildir 运行。我们必须小心与 Maildir 相关的额外的配置行添加到 `exim.conf` 文件中的顺序。

## 第 1 步

为了让 Maildir 与 Exim 工作，我们必须更改 `exim.conf` 文件中“Transports Configuration”部分默认的“local_delivery”选项。

更改“Transports Configuration”部分中的行。粗体文本是默认 exim.conf 文件中更改的内容。

- 编辑 exim.conf 文件（`vi /etc/mail/exim.conf`）并更改以下行：

```
local_delivery:

driver = appendfile

file = /var/mail/$local_part

delivery_date_add

envelope_to_add

return_path_add

group = mail

mode = 0600
```

修改为：

```
local_delivery:

driver = appendfile

check_string = ""

create_directory

delivery_date_add

directory = ${home}/Maildir/

directory_mode = 700

envelope_to_add

group = mail

dir_format

message_prefix = ""

message_suffix = ""

mode = 0600

return_path_add
```

### 第 2 步

现在，我们必须重启 Exim 守护进程使更改生效。

- 重启 Exim，使用以下命令：

```
[root@deep ~]# /etc/init.d/exim restart

Shutting down Exim: [OK]

Starting Exim: [OK]
```

## 将 aliases 文件中的 "postmaster" 设置为远程地址

由于服务器上的本地用户无法再次接收邮件，我们必须将 `/etc/mail/aliases` 文件中的 "postmaster" 别名更改为邮件枢服务器（Mail Hub Server）远程系统管理员，该管理员应接收所有生成的本地邮件。

### 第一步

在示例中，我使用了在本章之前创建的 aliases 定义，并将 "postmaster" 别名更改为中央邮件枢服务器上的人类邮箱地址，该地址应接收从空客户端邮件服务器（Null Client Mail Server）生成的所有本地邮件。加粗的文本是我从原始 aliases 文件中修改的内容。

- 编辑 aliases 文件（`vi /etc/mail/aliases`）并修改以下行：

```
# The following aliases are required by the mail RFCs 2821 and 2822.

# At least, you should set "postmaster" to the address of a HUMAN

# who deals with this system's mail problems.

postmaster:      sysadmin@domain.com

mailer-daemon:  postmaster

root:            postmaster

# It is a good idea to redirect any messages sent to system accounts

# so they don't just get ignored.

bin:            root

daemon:        root

sync:           root

mail:           root

uuccp:          root

ftp:            root

nobody:         root

www:            root

named:          root

postgres:       root

mysql:          root

squid:          root

amavis:         root

operator:      root

abusese:         root

hostname:      root

webmaster:     root
```

读取后：

```
# The following aliases are required by the mail RFCs 2821 and 2822.

# At least, you should set "postmaster" to the address of a HUMAN

# who deals with this system's mail problems.

postmaster:      markus@mailhubserver.com

mailer-daemon:  postmaster

root:            postmaster
```

```
# It is a good idea to redirect any messages sent to system accounts

# so they don't just get ignored.

bin:            root

daemon:        root

sync:           root

mail:           root

pop:            root
```

```
uucp: root

ftp: root

nobody: root

www: root

named: root

postgres: root

mysql: squid

amavis: root

operator: root

abuse: root

hostmaster: root

webmaster: root
```
