
`Domain=[ELIOT] OS=[Unix] Server=[Samba 3.0.14a-Ubuntu]`

`smb: >`

你会知道成功了，因为你会处于 Samba 提示符 `smb: >`。注意你会被提示密码。假设 `scott` 用户的密码是 `123456`（这是一个糟糕的密码，但只是假设），你可以输入此命令，而不会被提示密码：

```bash
$ smbclient //eliot/documents -U scott%123456
```

然而，这是一个极糟糕的主意，因为任何查看你的 `.bash_history` 文件（在“查看命令行历史”节讨论）的人都能看到。

### 表 16.1 smbclient

| Command | Meaning |
| :--- | :--- |
| `cd` | 切换目录 |
| `exit` | 关闭连接 |
| `get` | 获取文件 |
| `help` | 获取帮助 |
| `lcd` | 切换目录 |
| `ls` | 列出文件 |
| `mget` | 获取多个文件 |
| `mput` | 上传多个文件 |
| `put` | 上传文件 |
| `rm` | 删除文件 |

登录服务器后，只需输入 `help` 即可查看其他命令，但表 16.1 包含了基础。完成后，只需输入 `exit`，即可退出服务器并回到你的机器。

可以使用 `smbclient` 访问共享很酷，但如果你想使用 GUI 或想在共享上做大量工作，它也会很痛苦。在这些情况下，你应该使用 `smbmount`，它将共享挂载到你的本地文件系统，就像它是硬盘的一部分一样。挂载后，你可以打开你喜欢的文件管理器并轻松访问文件，甚至可以以最小的麻烦打开文字处理器等程序并打开文件。

要在你的文件系统上挂载 Samba 共享，必须创建一个挂载点，Linux 将共享挂载到那里。例如，如果你要挂载来自 `ELIOT` 的 `documents` 共享，你可以创建一个这样的目录：

```bash
$ mkdir /home/scott/eliot_documents
```

现在你运行 `smbmount` 命令以及一系列选项。

```bash
$ smbmount //eliot/documents /home/scott/eliot_docs -o credentials=/home/scott/bin/credentials_eliot,fmask=644,dmask=755,uid=1001,gid=1001,workgroup=TURING

smbmnt must be installed suit root for direct user mounts (1000,1000)

smbmnt failed: 1
```

在查看选项之前，让我们聊聊为什么 `smbmount` 失败了。第二行告诉了你原因：`smbmount` 用的 `smbmnt` 只能由 root 执行。如果你希望非 root 用户能够挂载 Samba 共享，这可能会是一个问题。解决办法是将 `smbmnt` 设置为 suit root（你在第 7 章的“设置并清除 suit”中学习过 suit）。

> **注意**：是的，你赋予了普通用户以 root 身份使用 `smbmnt` 的能力，但这并不是真的大问题。这绝对比给他们提供 root 密码或每当他们想挂载 Samba 共享时都需要你的参与要好得多。

以下是将 `smbmnt` 设置为 suit root 的方法。

```bash
smbmount

smumount
```

## 挂载 Samba 文件系统

```bash
ls /usr/bin/smbmnt
-rwxr-xr-x 1 root root /usr/bin/smbmnt

chmod u+s /usr/bin/smbmnt

ls -l /usr/bin/smbmnt
-rws-xr-x 1 root root /usr/bin/smbmnt
```

让我们再次尝试 `smbmount`。

```bash
smbmount //eliot/documents /home/scott/eliot_documents \
-o credentials=/home/scott/credentials_eliot,fmask=644,dmask=755,uid=1001,\
gid=1001,workgroup=TURING

ls -F /home/scott/eliot_documents/
presentations/ to_print/
```

让我们来过一遍你使用的命令。在 `smbmount` 之后，`//eliot/documents` 指定了你连接的 Samba 服务器和 Samba 共享。接着是你的挂载点路径 `/home/scott/eliot_documents`。`-o` 选项表示后面将是选项。

你可以使用 `credentials=/home/scott/credentials_eliot` 以外的任何以下内容：

- `username=scott,password=123456`
- `username=%123456`
- `username=scott`

第一种和第二种选择完全不安全，因为密码现在会出现在 `.bash_history` 和 `ps` 中。千万不要这样做！最后的选择会提示你输入密码，这是安全的，因为密码不会出现在 `.bash_history` 或 `ps` 中。但由于你正试图将挂载 Samba 共享的过程自动化，所以最后的选择也不行。

# 第 16 章 Windows 网络

现在只剩下 `credentials=/home/scott/credentials_eliot`。这告诉 `smbmount` 用户名和密码存储在一个文件中，格式如下：

```
username = scott
password = 123456
```

这与之前在“使用类似 FTP 的客户端访问 Samba 资源”中讨论过的凭据文件一样，并且像那个例子中一样，在创建凭据文件后使用 `chmod` 来严格限制可以查看该文件的人。如果你不在乎自动化登录过程，尽管可以使用 `username=scott` 并根据提示输入密码，这无疑是最安全的选项。

`fmask` 和 `dmask` 选项分别控制你在挂载 Samba 共享中创建的任何新文件和目录的默认权限。`644` 会为文件生成 `rw-r--r--`，而 `755` 会为目录生成 `rwxr-xr-x`。

注意：忘记我们在说什么了？回看第 7 章的“理解权限基础”。

记住所有的用户名和组名实际上都是数字的引用，你分别可以在 `/etc/passwd` 和 `/etc/group` 中看到它们。你当前机器上的用户 ID 数字可能是 `1000`，但在 Samba 服务器上，`1000` 可能是一个完全不同的用户，你的组 ID 也有同样的问题。通过 `uid=1001` 和 `gid=1001`，你告诉 Samba 服务器你在 Samba 上是谁。换句话说，你需要在 Samba 服务器的 `/etc/passwd` 和 `/etc/group` 中查找这些数字，而不是在本地机器上。如果你不这样做，可能会发现：

## 挂载 Samba 文件系统

你并不真正拥有它们，并且无法以你想要的方式使用它们。

最后，`workgroup=TURING` 指定工作组，这很显而易见。

共享挂载后，你可以打开文件管理器并开始浏览 `eliot_documents` 的内容，启动 `OpenOffice.org` 并直接打开 `eliot_documents/presentations/` 内部的文件，或者打开 `eliot_documents/to_print` 中的 PDF 并发送到打印机。如果你将以下行放在机器的 `/etc/fstab` 文件中，共享将自动挂载。

```
//eliot/documents /home/scott/eliot_documents smbfs -o credentials=/home/scott/credentials_eliot,fmask=644,dmask=755,uid=1001,gid=1001,workgroup=TURING 0 0
```

*（注：根据标准语法修正了 fstab 行中可能的 OCR 错误）*

警告：修改你的 `/etc/fstab` 文件时要非常小心，因为错误可能会导致系统无法启动。当然，你可以修复这个问题（请参阅我的书籍《Hacking Linux》获取技巧），但这仍然是一件痛苦的事，最好通过谨慎和小心来避免。关于 fstab 文件的更多信息，请查看系统上的 `man fstab`。

如果你决定不再访问 `eliot_documents` 的 Samba 共享，可以使用 `smbmount` 卸载它（注意是 unmount，不是 unmount）。

```bash
$ smbmount eliot_documents
smbmount must be installed suid root
```

太令人沮丧了！你还需要将 `smbmount` 设置为 suid root。

# 第 16 章 Windows 网络

```bash
$ ls -l /usr/bin/smbmount
```
