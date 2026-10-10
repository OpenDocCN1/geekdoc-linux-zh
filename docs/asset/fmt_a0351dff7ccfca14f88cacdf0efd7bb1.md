
# tripwire --check

```
======================================================================

Rule Summary:

======================================================================

... Section: Unix File System ...

Rule Name            Severity Level  Added  Removed  Modified

---------------      ----------------  -----  -------  --------

Invariant Directories        66        0        0        0

Sources                      100       0        0        0

Temporary directories        33        0        0        0

Tripwire Data Files          100       0        0        0

Local files                  100       0        8        0

Tripwire Binaries            100       0        0        0

Libraries, include files, and other system files

                            100       0        0        0

* System Administration Programs

                           66        0        0        1

User Utilities               100       0        0        0

X11R6                        100       0        0        0

NIS                          100       0        0        0

(/var/yp)

/ etc                        100       0        0        0

Security Control             100       0        0        0

Root's home                  100       0        0        0

FreeBSD Kernel               100       0        0        0

FreeBSD Modules              100       0        0        0

/dev                         100       0        0        0

Linux Compatibility

(/compat)

Total objects scanned: 466299

Total violations found:  1
```

你预期该文件与 Tripwire 预期的不同是有可能的；例如，你可能安装了更新版本的 `sshd`。每次更新 Tripwire 正在监控的文件时，你都应更新 Tripwire 数据库以反映新信息。你可以使用 `--update` 选项进行更新：

```
# tripwire --update
```

此命令重新运行整个 Tripwire 数据库生成过程，该过程扫描整个文件系统并写出一个使用你的站点和本地口令签名的更新数据库文件（当你运行该程序时，系统会提示你输入口令）。

如果你*真的*想要确保你的 Tripwire 数据库是安全的，并且你甚至不信任保护它的内置签名机制，你可以创建一个 Tripwire 软盘——将数据库放置在计算机之外的独立位置是确保数据完整性的最安全方法。

不幸的是，Tripwire 数据库太大，无法放入软盘；但是，你可以从 Tripwire“策略”中删除项目以减小数据库文件的大小。通过编辑 `/usr/local/etc/tripwire/twpol.txt` 来完成此操作，删除或注释掉指定你不想包含的文件位置的行，然后发出带有 `-m P`（或 `--create-policy`）参数的 `twadmin` 命令来保护实际的（非人类可读的）策略文件：

```
# twadmin -m P -S /usr/local/etc/tripwire/site.key
➜ /usr/local/etc/tripwire/twpol.txt
```
