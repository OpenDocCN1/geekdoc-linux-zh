

| 命令 | 描述 |
|---|---|
| `cd` | 更改远程目录 |
| `chmod` | 使用 Linux 权限更改远程文件的模式 |
| `chown` | 更改远程文件的所有者 |
| `close` | 关闭具有指定文件 ID 的打开文件 |
| `del` | 删除指定的文件 |
| `dir` | 列出远程目录的内容 |
| `exit` | 退出连接 |
| `get` | 获取指定的远程文件，将其保存为相同的文件名或第二个指定的文件名 |
| `help` | 列出 `smbclient` 命令 |
| `l` | 列出远程目录的内容 |
| `lcd` | 更改本地目录 |
| `ls` | 列出远程目录的内容 |
| `md` | 在当前远程目录下创建新目录 |
| `mget` | 根据指定的通配符模板从远程目录获取多个文件 |
| `mkdir` | 在当前远程目录下创建新目录 |
| `more` | 使用 Linux `more` 命令查看远程目录中的文件 |
| `mput` | 根据指定的通配符模板将多个文件从本地目录发送到当前远程目录 |
| `open` | 打开远程目录中的文件 |
| `put` | 将本地目录中的指定文件发送到当前远程目录 |
| `pwd` | 显示当前远程目录路径名 |
| `q` | 从服务器共享注销 |
| `rd` | 删除当前远程目录下的目录 |
| `reget` | 从远程目录获取文件，从现有本地文件位置的末尾重新开始 |
| `rename` | 重命名当前远程目录中的文件 |
| `reput` | 从现有远程文件位置的末尾开始发送文件 |
| `rm` | 删除当前远程目录中的指定文件 |
| `rmdir` | 删除当前远程目录下的指定目录 |
| `showconnect` | 显示当前服务器连接的信息 |
| `wdel` | 使用通配符模板删除一组远程文件 |
| `quit` | 从服务器共享注销 |

以下是 smbclient 会话中使用命令的示例：

```
rich@testbox:~$ smbclient //localhost/test -U test
Enter test's password:
Domain=[TESTBOX] OS=[Unix] Server=[Samba 3.2.3]
smb: \> dir
. D 0 Sat Nov 8 18:35:30 2008
.. D 0 Sat Nov 8 18:35:30 2008
.profile H 675 Sat Nov 8 18:35:30 2008
.bash_logout H 220 Sat Nov 8 18:35:30 2008
.bashrc H 3115 Sat Nov 8 18:35:30 2008

61335 blocks of size 131072. 47710 blocks available
smb: \> put test.txt
putting file test.txt as \test.txt (3.6 kB/s) (average 3.6 kB/s)
smb: \> dir test.*
test.txt A 44 Sat Nov 8 19:36:37 2008

61335 blocks of size 131072. 47710 blocks available
smb: \>
```

连接到 Samba 服务器上的共享后，我使用了 dir 命令列出共享中的文件。然后我使用 put 命令将文件 test.txt 从本地文件夹发送到共享文件夹，并再次使用 dir 命令以确保它确实已到达。

将文件发送到共享后，您也可以从 Ubuntu 命令行在文件夹中看到该文件：

```
rich@testbox:~$ ls -al /home/test
total 24
drwxr-xr-x 2 test test 4096 2008-11-08 19:36 .
drwxr-xr-x 4 root root 4096 2008-11-08 18:35 ..
-rw-r--r-- 1 test test 220 2008-11-08 18:35 .bash_logout
-rw-r--r-- 1 test test 3115 2008-11-08 18:35 .bashrc
-rw-r--r-- 1 test test 675 2008-11-08 18:35 .profile
-rw-r--r-- 1 test test 44 2008-11-08 19:36 test.txt
rich@testbox:~$
```

如预期，新文件确实在文件夹中。

> Secret
> 如果您使用 Samba 与 Windows 客户端共享 Ubuntu 文件夹，请注意文本文件。Ubuntu 和 Windows 使用略有不同的文本文件格式。Ubuntu 在每行末尾使用单个换行符，而 Windows 则使用回车控制字符以及换行符。如果您在 Samba 共享中保存 Windows 文本文件并尝试在 Ubuntu 中查看它，您可能会感到失望。
> 
> Ubuntu 提供了用于将 Windows 文本文件转换为 Linux 格式，反之亦然的一组实用程序。只需使用 apt-get 程序安装 tofrodos 包即可。

