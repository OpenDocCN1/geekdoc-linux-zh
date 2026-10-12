
```
# rpm -Uvh samba-3.6.0-g64pre1.fc15.i686.rpm

###################################### [100%]

Preparing...

###################################### [100%]

1:samba
```

安装软件包时，`rpm`文件必须位于工作目录，或者你必须使用指向该`rpm`文件的路径。如果你指定了FTP或HTTP URL，`rpm`将在安装前下载该软件包（但它不会下载或安装依赖项）：

```bash
# rpm -Uvh http://download.redhat.com/pub/fedora/linux/i386/bind-9.8.0-P2.fc15.i686.rpm
```

删除：以下命令移除`samba`软件包。你可以从任何目录执行该命令：

```bash
# rpm -e samba
```

```
error: Failed deleting dependencies: (installed) system-config-samba-1.29-2-fc15.noarch
```

当你运行此命令时，`rpm`报告另一个软件包`system-config-samba`依赖于`samba`软件包。要移除`samba`软件包，你有两个选择：可以通过包含`rpm --nodeps`选项来忽略依赖，或者先删除依赖包再删除`samba`软件包。

```bash
# rpm -e system-config-samba
# rpm -e samba
```
