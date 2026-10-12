
```python
fd2.write(linea)

ruta = "/samba/" + share_name

cmd = "mkdir -p " + ruta

print("Creating %s" % share_name)

output = subprocess.check_output(cmd, shell=True)

print output

fd2.write('\t')

fd2.write('path = \'')

fd2.write(ruta)

fd2.write('\n')

fd2.write('\tread only = Yes\n')

fd2.write('\tguest ok = No\n')

except Exception, e:

    print str(e)

fd2.close()
```

该程序在 `/samba` 文件夹中创建 Windows 共享（排除管理共享）。还会生成一个名为 `add_to_smb.conf` 的文本文件，包含要添加到 `/etc/smb/samba.conf` 的共享定义。执行非常简单。

```
[root@india ~]# ./mig_winshares.py shares_win.txt

Creating public
```

# 第 10 章 SAMBA 中的文件服务

在我们的示例中，创建了以下文本：

```
[root@india ~]# cat add_to_smb.conf

[public]

  path = /samba/public

  read only = Yes

  guest ok = No
```

这是应该添加到 Samba 配置文件中的共享定义。该共享最初被声明为只读，出于安全考虑，将不允许匿名访问。稍后我们需要应用正确的访问权限。

## 迁移目录和文件

一旦用户、组和共享迁移完成，就是时候迁移数据了；即每个共享内部的文件和目录。迁移数据的有用工具是 `smget`，它允许我们在 Windows/Samba 共享上执行递归下载。它的工作方式非常类似于 `wget`。在我们的案例中，我们已经移动到了 `/samba/public` 文件夹并使用正确的参数执行了 `smget`。

```
[root@india public]# pwd
/samba/public
[root@india public]# smget -R -u Antonio -p antonio smb://192.168.1.200/
public
```

不幸的是，CentOS 编译的 `smget` 二进制文件似乎有一个 bug，我们可能会遇到以下错误：

```
You don't have enough permissions to access smb://192.168.1.200/public/201801_data.txt
You don't have enough permissions to access smb://192.168.1.200/public/201802_data.txt
```

如果使用 `-d` 参数获取一些调试信息，我们将看到这些：

```
.
NTLMSSP_NEGOTIATE_128
NTLMSSP_NEGOTIATE_KEY_EXCH
SPNEGO login failed: NT_STATUS_LOGON_TYPE_NOT_GRANTED
".
.
```

显然，协商过程似乎存在问题。然而，这个 bug 似乎在较版本的 Samba 工具中修复。当我们学习 Samba 4 和活动目录时，我们将下载、编译并安装更新版本的 Samba（详情请参见第 17 章）。

如果我们启动 `smbget`，我们就能下载文件。

```
[root@india public]# /root/soft/samba-4.7.11/bin/smbget -R --user Antonio
smb://192.168.1.200/public
Password for [Antonio] connecting to //192.168.56.200:
Using workgroup LINUXAHOLICS, user Antonio
smb://192.168.1.200/public/20181_data.txt
smb://192.168.1.200/public/20182_data.txt
Downloaded 15b in 10 seconds
```

我们已经在 Samba 服务器中定义了共享并复制了内容。现在只需要调整权限并为 Samba 中的用户分配新密码。为了获取与 Windows 中共享文件相关的原始权限，我们可以使用 `smbcals`。

```
[root@hotel public]# smbcals //192.168.1.200/public 20181_data.txt -U antonio
antonio%Antonio
REVISION:1
CONTROL:SR|DI|DP
OWNER:ZULU\Antonio
GROUP:S-1-5-21-852636792-403353388-521036446-512
ACL:NT AUTHORITY\SYSTEM:ALLOWED/I/FULL
ACL:ZULU\Antonio:ALLOWED/I/FULL
ACL:BUILTIN\Administrators:ALLOWED/I/FULL
ACL:Todos:ALLOWED/I/READ
```

有了这些信息，我们可以编写另一个程序或脚本为每个共享应用正确的访问权限。

## 限制 IPC$ 的访问

IPC$ 是 Windows（以及 Samba）用于通过远程过程调用（RPC）进行进程间通信的特殊共享。连接的客户端可以在服务器上执行一系列操作，如列出用户、列出共享等。尽管如此，黑客也可以 IPC 创建匿名连接并获取服务器的信息。为了最小化这种风险，我们可以在 `/etc/samba/smb.conf` 文件中添加 IPC$ 条目并添加以下访问列表。

```
[IPC$]
hosts allow = 192.168.1.0/24
hosts deny = 0.0.0.0
```

## 处理文件共享用户和组的脚本

我们到为止已经看到，用户要成功连接到 Samba 共享，该用户必须在操作系统本身存在。当我们在本章之前学习文件服务时，我们使用了脚本在向本地 Samba 数据库添加这些用户之前创建相应的 Linux 用户。事实上，当我们使用 `tdb` 后端（参见第 8 章）时，如果尝试添加一个不存在的 Samba 用户，我们会收到以下错误：

```
[root@hotel ~]# smbpasswd -a Ivan
New SMB password:
Retype SMB password:
Failed to add entry for user Ivan.
```

然而，我们可以使用指令让 samba 服务在用户连接到 Samba 共享时自动创建 Linux 用户。这可以通过 `add user` 脚本参数实现，该参数默认没有值。

```
[root@hotel ~]# testparm -v | grep "add user"
Load smb config /etc/samba/smb.conf
rlimit_max: rlimit_max (1024) to minimum limit (16384)
Processing section "[homes]"
Processing section "[printers]"
Processing section "[Docs]"
Loaded services OK.
Server role: ROLE_STANDONE
Press enter to see dump of service definitions
add user script =
```

我们可以轻松地指向在前面情况下由 root 执行的脚本完整路径。例如：

```
add user script = /usr/local/samba/bin/add_user %u
```

同样适用于组的创建，在这种情况下参数是 `add group`。一个示例如下：

```
add group script = /sbin/groupadd %g
```
