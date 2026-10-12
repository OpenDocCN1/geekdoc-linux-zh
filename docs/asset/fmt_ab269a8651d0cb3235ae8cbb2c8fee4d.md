
# 第 16 章：创建文件服务器

为了尽量减少拼写错误的影响，在 Samba 文件中，`browseable` 是 `browsable` 的同义词。

以下指令建议了合适的、几乎是不言自明的选项。是的，来自主目录的共享可以设置为只读。新目录和文件的读、写、执行权限可以限制为主目录的所有者：

```
; read only = yes

; create mask = 700

; directory mask = 700
```

由于用户将对其主目录拥有写入权限，你可能希望设置以下指令；为了尽量减少拼写错误的影响，在 Samba 文件中，`writeable` 是 `writable` 的同义词。

```
writable = yes
```

以下指令限制访问与主目录关联的用户名：

```
; valid users = %S
```

我经常在此处添加类似这样的指令段来共享文件。请注意；方括号中的名称将显示为“共享目录”。你在这些括号之间包含的名称不需要匹配任何现有文件夹或目录。

```
[tmp]

comment = Temporary file space

path = /tmp

read only = no

public = yes
```

打印机目录——打印驱动程序默认是共享的。`[printers]` 共享不需要是可浏览或可写的，因为你不希望任何用户在打印池池目录中查看或写入普通文件：

```
[printers]

comment = All Printers

browseable = no

path = /var/pool/samba

printable = yes

guest ok = no

read only = yes

create mask = 0700
```

最后，有一个用于打印驱动程序的共享。如果 `/var/lib/samba/printers` 目录下存在微软打印驱动程序，微软客户端将能够安装这些打印驱动程序，而无需访问微软安装文件。写入权限限制为 Linux 和微软管理员用户。

```
[print$]

comment = Printer Drivers

path = /var/lib/samba/printers

browseable = yes

read only = yes

guest ok = no

write list = root, @ntadmb
```

## 测试 `/etc/samba/smb.conf` 的更改

在对 `/etc/samba/smb.conf` 进行更改后，在将其投入生产之前应该始终测试系统。你可以使用 `testparam` 命令对 Samba 配置文件进行简单的语法检查。这并不会实际检查服务是否运行或运行正常；它只检查基本的文本语法和指令段。

## 基础域成员

域成员将认证请求传递给其他。基础域成员的关键指令包括 `/etc/samba/smb.conf` 配置文件中的以下指令：

```
security = server

password server = <NT Server Name>
```

`password server` 指令应设置为具有认证数据库系统的主机或 IP 地址，通常是 PDC。在这种情况下，请相应替换 `<NT Server Name>`。或者，如果 `password server = *`，系统会自动搜索网络中的 PDC，但可能会延迟登录。

## 域控制器

如果该系统是 PDC 或 BDC，则 `/etc/samba/smb.conf` 配置文件中的 `security` 应如下设置：

```
security = user
```

通常，应该将 PDC 或 BDC 配置为主主，以方便进行 NetBIOS 搜索。

## 活动目录部分

在 Samba 4 发布之前，Samba 仅限于作为网络的成员服务器。为此，可以将 Samba 服务器配置为基础域成员，使用以下指令：

```
security = ads
```

## 实现更改

当然，更改必须通过 Samba 脚本来实现。在大多数情况下，使用以下命令重启脚本：

```
sudo /init.d/samba restart
```

我可以重新加载配置而不重启 Samba，这意味着现有的连接不会中断：

```
sudo /init.d/samba reload
```

当然，假设你已经解决了与密码相关的问题——除非你实现了 LDAP，否则无法使用与 Linux 网络相同的数据库。

## 图形化共享工具

如果尚未安装 NFS 或 Samba 服务器，并且启动了共享文件夹工具，将出现图 16-2 所示的窗口，提示安装 NFS 和 Samba。如果你是按顺序阅读本章，这些服务已经安装；否则，Samba 将连接到软件包管理器进行安装。已安装的 NFS 服务是内核。

## 准备共享

在开始之前，备份 `/etc/exports` 和 `/etc/samba/smb.conf` 文件的当前版本。最简单的选项是通过以下命令将这些备份到你的主目录：

```bash
cp /etc/exports ~
cp /etc/samba/smb.conf ~
```
