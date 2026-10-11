
```
$ IF $PMODE() == .NE . "INTERACTIVE" THEN GOTO ENDINTER
$ $1$ 将你只想在交互式登录时执行的命令
$ $1$ 放在此注释与 "ENDINTER" 符号之间。
$ IF $1 == /EDIT/CMD/COMMON:$SYSLOGIN:ETHI.L
$ SHUTDOWN == "$SYSSYSTEM:$SHUTDOWN" THEN SHUTDOWN YES NO LATER NO HONE
$ REBOOT == "$SYSSYSTEM:$SHUTDOWN" THEN SHUTDOWN YES NO LATER YES HONE
$ SHUTDOWN == "$SYSSYSTEM:$SHUTDOWN"
$ PWRSMAGER===$SYSMANAGER:PFILE.COM
$ PWRSMAGER===$SYSMANAGER:PWRKSHOWYS.COM
$ APACHEON==="$SYSSTARTUP:APACHESTARTUP.COM"
$ APACHEOFF==="$SYSSTARTUP:APACHESHUTDOWN.COM"
$ ENDINTER:
$ IF $PMODE() == .BATCH THEN GOTO ENDBATCH
$ $1$ 将你只想在批模式下执行的命令放在此注释
$ $1$ 与 "ENDBATCH": 符号之间。
```

图 8-43 在文件 `SYSCOMMON:` 中添加 `APACHE` 和 `APACHEEOFF` 行，这样系统管理员登录时就可以轻松地开启或关闭 Apache！

| 缓冲区: LOGIN.COM | 插入 | 进 |
| --- | --- | --- |
| 已写入 29 行到文件 SYSCOMMON:[SYSMGR]:LOGIN.COM;5 | | |

第 8 章 – Apache VMS 和 Linux 风格 177

![](img/3ba916f144e94350147c366c3485e02e_176_0.png)

图 8-44 编辑 `SYLOGICALS.COM` 文件，该文件在系统引导/启动时定义系统本地变量。

![](img/3ba916f144e94350147c366c3485e02e_176_1.png)

图 8-45 定义 "home" 逻辑，以便 VM 用户可以从主目录/登录目录使用 Apache。

Linux 与 OpenVMS 互操作性

```
File Edit Commands Options Print                                                                                             Help
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
$
  DIR USER$HOME:[OPCOM]*.DIR
Directory USER$HOME:[OPCOM]
PUBLIC_HTML.DIR;1  STOR.DIR;1
```

共 2 个文件。

图 8-46 用户可以（从其登录目录）创建一个名为 `[.PUBLIC_HTML]` 的子目录，该目录可以包含他们的个人主页或任何想要在 Apache 主目录中提供的 Web 页面。你可以通过浏览器从 `http://vsmsone/~-opcom` 添加个人 Web 页面，以访问这些或其他用户的 Web 文件。

![](img/3ba916f144e94350147c366c3485e02e_177_0.png)

```
File Edit Commands Options Print                                                                                             Help
DIRECTORY USER$HOME:[OPCOM].PUBLIC_HTML
3199COMM_TRUCK_LARGE.JPG;1  3199COMM_TRUCK_LARGES.JPG;2;JPG;2
5TOWRN9.JPG;2  5TOWRN9.JPG;1  ACSTR001.JPG;2  ACSTR002.JPG;2
ACSTR003.JPG;2  ACSTR004.JPG;2  ACSTR005.JPG;2  ACSTR006.JPG;2
ACSTR007.JPG;2  ACSTR008.JPG;2  ACSTR009.JPG;2  ACSTR010.JPG;2
ACSTR011.JPG;2  ACSTR012.JPG;2  ACSTR013.JPG;2  ACSTR014.JPG;2
ALLCHORT.PDF;2  AH-GC-7.JPG;2  APALL001.JPG;2  APALL002.JPG;2
BACKGROUND042.BMP;1  BACKGROUND042.JPG;1  BUKSHOT001.JPG;2  BUKSHOT002.JPG;2
BIHLDAHL1_SCORNE.JPG;2  BLXD001.JPG;2  BLXD002.JPG;2  BLXD004.JPG;2
BLXD010.JPG;2  BLXD105.JPG;2  BLXD006.JPG;2  BLXD007.JPG;2
BLXD008.JPG;2  BLXD009.JPG;2  CBUFF072.JPG;2  CBUFF074.JPG;2
DEAFHR001.JPG;2  DEAFHR011.JPG;2  DEAFALP001.JPG;2  DEAFBR001.JPG;2
DEFPW001.JPG;2  DEFPW101.JPG;2  DEFTTP001.JPG;2  DEFTM001.JPG;2
DEFTOP001.JPG;2  EBERASE001.JPG;2  ELLOGIC001.JPG;2
DEFOWMAC.ZIP;2  ELGAR001.JPG;2  ELGAR800_V1.JPG;2  APC125c01.JPG;2
EB_BLN90.JPG;2  EB_HTML.JPG;2  FAICON.ICO
MARKET001.JPG;2  PWRKS.JPG;2  GRID106.JPG;1
RETURN/Space+More,NEXT/Scroll,Home,SELECT*Ctrl+Quit
```

图 8-47 确保每个用户的子目录包含一个 `INDEX` 文件。可以通过浏览器查看并检索 `INDEX` 文件的文件。

第 8 章 – Apache VPS 和 Linux 风格 179

![](img/3ba916f144e94350147c366c3485e02e_178_0.png)

8-49 从此过程获取默认值以运行 Apache（至少一次）。

Linux 与 OpenVMS 互操作性

```
$ osysmanager:apache$config
```

```
$ osysmanager:apache$config
```

Compaq Secure Web Server for OpenVMS Alpha 此过程帮助你定义在系统上运行 Compaq Secure Web Server 所需的参数和环境。

请提供安装包的设备和目录。[SYS$COMMON:APACHE]

安装包的设备和目录？[SYS$COMMON:APACHE]

请提供特定系统的设备和目录。集群中的每个系统都有自己的写入特定文件的逻辑名称（例如日志文件）。此处指定的设备和目录将被系统使用。该命令将创建特定的目录和必要的子目录。你不需要手动创建这些。

系统的设备和目录？[SYS$COMMON:APACHE.SPECIFIC.VMSONE]

![](img/3ba916f144e94350147c366c3485e02e_179_0.png)

请提供安装包的设备和目录。

安装包的设备和目录？[SYS$COMMON:APACHE]

集群中的每个系统都有自己的写入特定文件的逻辑名称（例如日志文件）。此处指定的设备和目录将排除此系统。该命令将创建特定的目录和必要的子目录。你不需要手动创建这些。

系统的设备和目录？[SYS$COMMON:APACHE.SPECIFIC.VMSONE]

你可以指定一个在服务器启动之前执行的可选启动过程。

如果你没有指定启动过程，默认启动过程 `APACHESH:[000000]APACHESERVER_STARTUP.COM` 将执行。

系统未定义服务器启动。

更改服务器启动？[NO] yes

服务器启动过程（可选）？[NONE]

图 8-50 启动服务器/服务回答 yes。

![](img/3ba916f144e94350147c366c3485e02e_179_1.png)

系统的设备和目录？[SYS$COMMON:APACHE.SPECIFIC.VMSONE]

你可以指定一个在服务器启动之前执行的可选启动过程。

如果你没有指定启动过程，默认启动过程 `APACHESH:[000000]APACHESERVER_STARTUP.COM` 将执行。

系统未定义服务器启动。

更改服务器启动？[NO] yes
