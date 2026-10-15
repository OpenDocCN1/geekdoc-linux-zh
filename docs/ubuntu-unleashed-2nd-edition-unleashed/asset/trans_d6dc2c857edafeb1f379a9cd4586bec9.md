
作为通配符，允许yourdomain.com中的所有主机访问/file/system。第三个共享允许C类网络192.15.69.0的所有主机访问/file/share。出于安全考虑，最好不要在互联网上使用像最后两种这样的共享，因为数据经过的任何网络都可以读取所有数据。

## 表22.1 /etc/fstab选项

| 选项 | 用途 |
| --- | --- |
| rw | 提供读写访问权限 |
| ro | 提供只读访问权限 |
| async | 当服务器（而非客户端）认为需要时写入数据 |
| sync | 收到数据时立即写入 |

以下是一个/etc/exports文件的示例：

```
# /etc/exports: the access control list for filesystems which may be exported
# to NFS clients. See exports(5).
/home/andrew 192.168.2.1/24(rw,no_root_squash)
```

该文件将/home/ahudson导出（共享）给192.168.2.*中的任何主机，并允许用户读写/home/ahudson。

完成/etc/exports文件的编辑后，以下命令

```
sudo exportfs -a
```

会将/etc/exports文件中的所有文件系统导出到/var/lib/nfs目录下名为xtab的列表中，当远程计算机请求导出目录时，该列表用作挂载指南。命令的-r选项会读取整个/etc/exports文件并挂载所有条目。你也可以使用exportfs命令临时导出特定文件。以下是使用exportfs导出文件系统的示例：

```
/usr/sbin/exportfs -o async yourhost:/usr/tmp
```

此命令使用async选项将/usr/tmp导出到yourhost。

确保在对/etc/exports进行任何更改后重启NFS服务器。如果你愿意，可以在使用X Window System时使用Ubuntu的shares-admin图形客户端来设置NFS。单击“系统”菜单，然后从“管理”菜单中选择“共享文件夹”菜单项即可启动该客户端。你也可以在X终端窗口的命令行中启动该客户端，如下所示：

```
$ gksudo shares-admin &
```

按Enter键后，系统会提示你输入密码。输入密码并单击“确定”；随后主窗口将显示。单击“添加”按钮打开“添加共享”对话框，如图22.1所示。

![](img/e464b828c497c99e41f61d4c55f1c0db_543_0.png)

图22.1 你可以使用Ubuntu的share-admin客户端快速设置使用NFS导出的本地目录。

在“路径”下拉框中选择要共享的目录；在“共享”下拉框中选择NFS。单击出现的“添加主机”按钮，以指定允许访问该目录的主机、IP地址或网络。默认情况下，目录以读/写方式导出，但你可以通过勾选“只读”选项来选择只读。完成后，单击“确定”按钮，再单击“应用”按钮，然后使用“文件”菜单退出。

## NFS客户端配置

要将主机配置为NFS客户端（以获取远程文件或目录），请像挂载任何本地文件系统一样编辑/etc/fstab文件。但是，不要使用要挂载的设备名（如/dev/hda1），而是输入远程主机名和要导入的文件系统。例如，一个条目可能如下所示：

```
# Device        Mount Point    Type    Options        Freq Pass
yourhost:/usr/local    /usr/local    nfs    nfsvers=3,ro    0    0
```

注意

> 如果你的系统使用autofs，则需要为远程NFS挂载使用正确的autofs条目。参见autofs的第5部分手册页。

“选项”列使用与标准fstab文件条目相同的选项，并增加了一些附加条目，如指定NFS第三版本的nfsvers=3。你还可以以root身份使用mount命令，通过远程主机名和导出的目录快速将远程目录附加到本地文件系统。例如：

```
$ sudo mount -t nfs 192.168.2.67:/music /music
```

按Enter键后，整个远程目录会出现在你的文件系统中。你可以使用df命令验证导入的文件系统，如下所示：
