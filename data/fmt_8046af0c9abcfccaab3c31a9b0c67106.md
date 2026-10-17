
```
A:\>dir

Volume in drive A is FLOPPY

Directory of A:\

FILE1 TXT        99 10-05-99  2:19p FILE1.TXT

LONGFI~1.TXT     99 10-05-99  2:21p LongFilename.txt

               5 file(s)           198 bytes
```

名为 `LongFilename.txt` 的文件还带有改名后的文件名 `LONGFI~1.TXT`，DOS 和不理解长文件名的旧版 Windows 程序使用它。Samba 支持类似的功能，即使在不包含显式名称改名支持的文件系统上也是如此。

### NOTE

> 在 Windows 中，VFAT 和 NTFS 文件系统提供对名称改名的直接支持。即使使用 VFAT 或 NTFS，Samba 的名称改名也是自行生成的。因此，你在 Samba 共享中看到的改名名称与直接访问同一 FAT 或 NTFS 磁盘或从 Windows 服务器访问时看到的名称不同。如果你让服务器在 Linux 和 Windows 之间双启动，DOS 客户端因此会看到非 8.3 兼容名称的不同文件名。

影响名称改名和大小写敏感性的 Samba 选项包括以下内容：

- `mangled names`—此选项的默认值为 yes。如果将此选项设为 no，Samba 不执行名称改名；它只是截断文件名，这可能导致两个文件具有相同名称。发生这种情况时，你只能访问其中一个文件。
- `mangle case`—转换文件的大小写，通常向客户端提供全大写名称。默认值为 no。
- `case sensitive`—如果此选项设为 yes，Samba 以区分大小写的方式处理文件名。默认值为 no，这要求 Samba 做更多工作来匹配文件名。
- `default case`—此选项指定来自不区分大小写客户端的新文件的默认大小写。默认值为 lower。
- `preserve case`—如果此选项设为 yes（默认值），它会保留来自保留大小写 OS 的大小写，例如 Windows 和 OS/2。如果设为 no，文件名将被转换为默认大小写。

## Samba 守护进程

像大多数网络服务一样，Samba 通过运行守护进程（p. 62）来操作。Samba 包包含两个守护进程：

- `smbd`—SMB 守护进程提供了你想到 Windows 网络时所想到的绝大部分服务，包括至关重要的文件交换服务。
- `nmbd`—名称浏览器守护进程负责在 NetBIOS 网络上宣布你的 Linux 服务器的存在。如果它未正确配置，你将无法从 Windows 访问 Linux 计算机的共享。

运行 Samba 守护进程有两种方式：独立运行和从 inetd 运行。每种方式都有其优缺点。

## 独立运行 Samba

如果你输入 `ps ax | grep mbd -`，你会得到一份包含名称中带有字符串 mbd 的正在运行服务的报告。这包括两个 Samba 守护进程，通常不会有其他内容。

以下是我的系统中的一些示例输出：

```
8243 ?  S  0:00 smbd -D
8254 ?  S  0:00 nmbd -D
```

> 如果你看到多个 `smbd` 实例也不必担心。如果有多个客户端连接到 Samba 共享，这种情况是正常的。

由于输出中同时出现了 smb 和 nmb，很明显两个守护进程都在独立运行。不过，你是如何达到这种状态的呢？

许多 Linux 发行版，包括 Red Hat Linux 6.0，都在脚本 `/etc/rc.d/init.d/smb` 中启动 Samba 守护进程，该脚本接受参数 start、stop、restart 和 status。因此，如果 Samba 尚未运行，你可以输入 `/etc/rc.d/init.d/smb start` 来启动它。初始化脚本会在系统启动时运行 smb 脚本，所以在你安装 Samba 并重新启动后，它应该处于运行状态。

> 如果你安装了 Samba 并重新启动但它未运行，请检查 `/etc/rc.d/init.d` 和 `/etc/rc.d/rc5.d` 中是否存在名为 smb 的链接，指向 `/etc/rc.d/init.d/smb`。如果没有此类链接，请通过输入 `ln -s /etc/rc.d/init.d/smb /etc/rc.d/rc3.d` 和 `ln -s /etc/rc.d/init.d/smb /etc/rc.d/rc5.d` 来创建它们

在某些 Linux 发行版上，你可能需要通过编辑其他初始化脚本，例如 `/etc/rc.d/rc.local` 来启动 Samba。你可以在任何方便的启动脚本中添加类似以下的行：

```
/usr/sbin/smbd -D
/usr/sbin/nmbd -D
```
