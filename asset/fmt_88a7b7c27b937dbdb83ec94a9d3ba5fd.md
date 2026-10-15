
你必须使用文本编辑器修改示例配置文件中的设置，以匹配你的系统。处理器类型和显卡等项目必须与系统匹配。

> 注意：你也可以从硬盘分区启动 DOSEMU，而不是软磁盘。要访问硬盘，只需在 `dosemu.conf` 文件中配置驱动器/分区。

# 运行 DOSEMU

要运行 DOSEMU，只需在任何 Linux 提示符下输入 `dos`。要退出，请在提示符中使用 `exitemu` 命令。表 5.9 提供了传递给 DOSEMU 的命令行选项列表。你也可以使用 `-?` 获取完整且最新的命令行参数列表。

| 参数 | 说明 |
|---|---|
| -A | 从 A 盘启动 |
| -C | 从硬盘启动 |
| -C | 优化虚拟终端的视频性能 |
| -D | 设置调试选项 |
| -E | 指定 EMS 内存量 |
| -F# | 指明从 `dosemu.conf` 中使用的软磁盘数量 (#) |

# 在 Linux 下运行 DOS 程序 135

| 参数 |  |
|---|---|
| -f | 翻转 A 盘和 B 盘软字的定义 |
| -H# | 指明从 `dosemu.conf` 中使用的硬盘数量 (#) |
| -k | 使用 `dosemu.conf` 中 `rawkeyboard` 参数定义的原始控制台 |
| -P | 将调试信息复制到文件 |
| -t | 传递时间中断 9 |
| -V | 激活 VGA 仿真 |
| -x | 指定 XMS 内存量 |
| -? | 显示每个命令的摘要帮助 |
| -2 | 模拟 286 |
| -3 | 模拟 386 |
| -4 | 模拟 486 |

从 DOSEMU 提供的 DOS 提示符中，你可以运行大多数 DOS 程序，但需要 DPMIDOS（保护模式接口）的程序除外。只需输入程序名称——只要 DOSEMU 能在你的路径中找到该程序——DOSEMU 就会加载并运行该程序。

表 5.10 显示了一些已知在 Linux 下运行的程序，但每天都有新程序加入（请检查 DOSEMU 安装目录下的 `EMSUccess.txt` 文件以获取最新列表）。表 5.11 列了一些无法在 Linux 下运行的程序。

| 表 5.10 已知可在 DOSEMU 下运行的程序 |
| 名称 | 功能 | 案例发布者 |
| ------|---|---|
| 1st Wordplus | GEM 文字处理器 | jan@janhh.hanse.de |
| 4desc | 4dos desc 编辑器 | piola@di.unito.it |
| 4DOS 4.2 | 命令解释器 | rideau@clipper.ens.fr |
| 4dos 5.0c | 命令解释器 | J1MCPHER@VAXC, STEVENS-TECH.EDU |
| ack3d | 3-D 引擎 | martin5@trcorp.solucorp.qc.ca |
| ACU-COBOL | 编译器 | fjh@munta.cs.mu.OZ.AU |
| Alite 1.10 | | ph99jh42@uwrf.edu |
| AmTax 93 & 94 | 税务软件 | root@bobspc.canisius.edu |

# 表 5.10 继续

| 名称 | 功能 | 案例发布者 |
| --- | --- | --- |
| ansi.sys | 屏幕/键盘驱动程序（显示功能） | ag173@cleveland.Freeiten.Edu |
| arj v2.a1a | [解]归档程序 | tanner@winteret.mpls.mn.us |
| As Easy As 5.01 | 电子表格 | ph99jh42@uwrrf.edu |
| Autoute Plus | 路线规划器 | hsw1@papa.atlas.com |
| Axum | 科学图形 | miguel@pinon.ccu.uniov.ies |
| battle chess | 国际象棋游戏 | jvdbergh@wins.ia.ac.be |
| Binkley 2.50eebd | Fidomailer | stub@linux.tu-clausthal.de |
| Blake Stone_ | 游戏 | owadell@cs.indiana.edu |
| bnu 1.70 | Fossil (Fido) | stub@linux.tu-clausthal.de |
| Borland C++ 2.0 | 86/286 C++ | rideau@clipper.ens |
| Boston Business | | keepeg@csdr2.fs |
| Cardbox Plus | 数据库 | hsw1@papa.atlas.com |
| Castle Wolfenstein | 3-D 游戏 | gt8134@prism.gate |
| Checkit | | |
| classifier 5.1 | 编译器 | jvdbergh@wins.ac.be |
| COMPRESS | 压缩 fs | rideau@clipper.ens |
| CCM (Crosstalk) | 现代程序 | |
| cshow 8.61 | 图片查看器 | jvdbergh@wins.ac.be |
| cview | 图片查看器 | lotov@avarice.ugcs |
| d86/a86 | | |
| DataPerfect 2.1 | 数据库 | fbennett@uk |
| Dbase 4 | | corey@iganet.net |
| Derive 1.2 | 数学包 | miguel@pinon.ccu.uniov.ies |
| Disk Freedom 4.6 | 磁盘工具 | |
| diet 1.45 | 文件压缩 | stub@linux.tu-clausthal.de |
| dosnix 2.0 | UNIX 工具集 | miguel@pinon.ccu.uniov.ies |
| Dosshell | 交换器 | jmacleon@fox.ca |
| dttmm | 分子模型 | miguel@pinon.ccu.uniov.ies |

# 在 Linux 下运行 DOS 程序

| 名称 | 功能 | 案例发布者 |
|---|---|---|
| Dune 2 | 游戏 | COLIN@fs1.in.umist.ac.uk |
| dviscr | EMTEX dvi 预览 | ub9x@rz-karlsruhe.de |
| Easyxtrax | 布局编辑器 | maehler@wrcd1.uppertal |
| Elvis | vi 克隆版 | miguel@pinon.ccu.uniov.ies |
| Epic Pinball | 游戏 | krismon@quack.com |
| ETen 31 | 中文终端 | tyuan@mp.cs.edu |
| Eureka 1.0 | 数学包 | miguel@pinon.ccu.uniov.ies |
| Falcon 3.0 | 战斗模拟器 | rapatel@rockypc.rutgers.edu |
| FastLST 1.03 | Fidodel编译器 | stub@linux.tu-clausthal.de |
| FormGen II | | root@bobspc.canisi.edu |
| freemacs 1.6d | 编辑器 | ph99jh42@uurwf.de |
| Frontier (Elite II) | 游戏 | COLIN@fs1.in.umist.ac.uk |
| FW3 | | Sebastian.Bunka@vu-wien.ac.at |
| MS Flight Simulator 5 | 游戏（运行缓慢！） | newcomer@aa.csc.pocketnet.net |
| Foxpro 2.0 | 数据库 | corey@amiganet.net |
| Freelance Graphics 2.1 | 图形/绘画应用 | jwest@jwest.ceen.okstate.edu |
| GEM/3 | GUI | jan@janhh.hanse.de |
| GEM Draw | GEM 绘画应用 | jan@janhh.hanse.de |
| GEM Paint | GEM 绘画应用 | jan@janhh.hanse.de |
| gmouse | 鼠标驱动程序 | tk@pssparc2.co.com |
| God of Thunder | 游戏 | ensor@cs.uk.utku |
| Gravity | 模拟包 | miguel@pinon.ccu.uniov.ies |
| GWS for DOS | 图形文件转换 | bchow@bchow.slip |
| Gzip 1.1.2 | 文件压缩 | miguel@pinon.ccu.uniov.ies |
| Harpoon | 游戏 | wielinga@physics.uq.oz.au |
| Harvard Graphics 3.0 | 图形/绘画包 | miguel@pinon.ccu.uniov.ies |

# 第5章 运行 Linux 应用程序

| 名称 | 功能 | 案例发布者 |
| --- | --- | --- |
| Hero's Quest I | 游戏 | lam836@cs.cuhk.hk |
| Hijak 2.0 | 图形文件转换 | bchow@bchow.slip |
| hocus focus | Apogee 游戏 | kooper@dutiws.TWI.TUDelt.NL |
| Image Alchemy Pro | 图形文件转换（-V 不工作） | JM1MCPHERVAXC. STEVENS-TECH.EDU |
| Incredible Machine | 游戏（缓慢） | sdh@po.cwru.edu |
| Key Spreadsheet Plus | 电子表格（在非双速网格上） | jwest@jwest.ecen.okstate.edu |
| Lemmings | | sdh@po.cwru.edu |
| less 1.7.7 | 比 more 更多 | miguel@pinon.ccwu.uniovies.es |
| LHA | 文件压缩 | miguel@pinon.ccwu.uniovies.es |
| Lotus Manuscript | 文字处理器 | |
| Managing Your Money Manifest | 财务（在内存定时期间） | newcome@aa.cs.peachnet.com hsw1@papa.attmail.com |
| MathCad 2.01 | 数学包 | root@bobspc.canisi.edu |
| MathCad 2.06 | 数学包 | miguel@pinon.ccwu.uniovies.es |
| mcafee 9.23 v11 | 病毒扫描器 | jvdbergh@wins.uia.be |
| Microemacs | 编辑器 | hjsteinin@MATH.HUAC.IL |
| MicroLink Yaht 2.1 | | root@bobspc.canisi.edu |
| Microsoft C 6.0 | 编译器 | ronnie@epact.se |
| Microsoft Assembler 5.0 | 汇编器 | ronnie@epact.se |
| Microsoft Library 2.0 | | root@bobspc.canisi.edu |
| Microsoft Make | make | ronnie@epact.se |
| MicrosoftMouse Drv 8.2 | 鼠标驱动程序 | hsw1@papa.attmail.com |
| MoneyCounts 7.0 | 财务包 | raeburn@cygnus.com |
| mscmouse | 鼠标驱动程序 | tk@psprarc2.com |
| nnansi.com | ANSI 驱动程序 | mdrejhon@undergrad.math.uwaterloo.ca |

# 在 Linux 下运行 DOS 程序 139

| 名称 | 功能 | 成功案例发布者 |
|---|---|---||
| Netzplan | GEM 项目经理 | jan@janhh.hanse.de |
| NHL Hockey | 球游戏 | kismon@quack.kfu.com |
| NJStar 2.1 | 中文文字处理 | aab2@cornell.edu |
| Norton Utils 4.5 | 磁盘工具 | rideau@clipper.ens.fr |
| Norton Utils 7.0 | 磁盘工具 | rideau@clipper.ens.fr |
| PAF | 谱系包 | geek+@CMU.EDU |
| Paradox | 数据库 | hp@vmars.twien.ac.at |
| PC Paintbrush IV | 绘图程序 | bchow@bchow.slip |
| PCctools 4.20 | 磁盘工具 | rideau@clipper.ens.fr |
| pcwdemo | | |
| PC-Write 3.0 | 文字处理器 | |
| pcxlab 1.03 | PCX 查看器 | miguel@pinon.ccu.uniov.ies |
| peachtree complete 6.0 | 会计 | stjeanp@math.edu |
| Pinball Dreams | 游戏 | ronnie@lysator.liu.se |
| PKzip/unzip | 文件压缩 | |
| pklite 1.15 | 文件压缩 | stub@linux.rz.to-clausthal.de |
| Pong Kombat | 游戏 | ensor@cs.utk.edu |
| PrintShop | 贺/问候卡包 | geek+@CMU.EDU |
| Procomm Plus 2.0 | 通信 | newcombe@aa.csc.peachnet.edu |
| Procomm 2.4.3 | 通信 | hsw1@papa.atlas.com |
| Pspice 5.0 | 电路仿真 | root@bobspc.canisi.us |
| Q&A | 文字处理/数据库 | newcombe@aa.csc.peachnet.edu |
| Qbasic/edit | 解释器（来自 DOS 5.0） | |
| Qedit | 编辑器 | martin@trcsun3.eas.asu.edu |
| Quicken 4.0 for DOS | 会计包 | juphoff@nrao.edu |
| Quicken 6.0 for DOS | 会计包 | |
| Quicken 7.0 for DOS | 会计包 | juphoff@astro.phys.vt.edu |
| Railroad Tycoon | | juphoff@astro.phys.vt.edu |

## 表 5.10 续

| 名称 | 功能 | 成功案例发布者 |
|---|---|---|
| Red Baron | 游戏 | wielinga@physics.uq.oz.au |
| RM/COBOL | 编译器 | fjh@munta.cs.mu.OZ.AU |
| Rpro 1.6 | | root@bobspc.canisius.edu |
| scan109 | 杀毒软件 | miguel@pinon.ccu.uniovies |
| scan112 | 杀毒软件 | piola@di.unito.it |
| Scorch | 坦克游戏 | geek@CMU.EDU |
| Shez94 | 存档-壳 | stub@linux.rz.tu-clausthal.de |
| sled | 编辑器 | piola@di.unito.it |
| Space Quest IV | 游戏 | lam836@cs.uhuk.hk |
| Spell Casting 301 | | mancini@phantom.com |
| SPSS/PC+4.0 | 统计包 | jr@petz.han.de |
| Squish 1.01 | Fido 扫描/投递 | stub@linux.rz.tu-clausthal.de |
| Stacker 3.1 | 压缩文件系统 | mdrejon@undergrad math.waterloo.co |
| Stacker 4.00 | 压缩文件系统 | J1MCPHER/VAXC. STEVENS-TECH.EDU |
| StatPhys | 仿真包 | miguel@pinon.ccu.uniovies.edu |
| STSORBIT | 轨道仿真 | troch@gandalf.rutgers.edu |
| Stunts | 游戏？ | gt8134b@prism.gatech.EDU |
| Superstar | 压缩文件系统 | rideau@clipper.ens.fr |
| TAG 2.02 | 波兰语文字处理 | rzm@oso.osmalmers.com |
| TASM 2.51 | 宏汇编器 | rideau@clipper.ens.fr |
| Telix | 现代程序 | jou@nematic.ep.netu.edu.tw |
| THelp from BC++2.0 | 弹出帮助 | rideau@clipper.ens.fr |
| TimEd/beta | Fido MSGetidor | stub@linux.rz.tu-clausthal.de |
| TLINK 4.0 | 链接器 | rideau@clipper.ens.fr |
| Topspeed Module-2 | 编译器 | mayersn@hermes. informatik.uni-stuttgartart.de |
| Turbo Debugger 2.51 | 实模式调试器 | rideau@clipper.ens.fr |
| Turbo Pascal 5.5 | 编译器 | |

# 在 Linux 下运行 DOS 程序

| 名称 | 功能 | 成功案例发布者 |
|---|---|---|
| Turbo Pascal 6.0 | 编译器 | t2262dj@cd1.muenchen.de |
| Turbo Pascal 7.0 | 编译器 | mdrej@under...... |
| Turbo-- | | |@....... |

| | | |........ |

|| . | | |@..uerburg.edu |
| Warrior of Destiny | 游戏 | bucket@uk |
| Windows 3.0 | 游戏 | j1@.... |
| 33 | | | |.... |

| | | | |.......

| | | | | | |.....edu |
| WordPerfect 6.0 | 文字处理器 | juphoff@astro.vt.edu |
| NON UTILITIES 7.0 | 磁盘工具 | rideau@clipper.ens.fr |
| Quattro Pro 4.0 | 表格软件 | jwest@okstate.edu |
| Raptor | 游戏 | ensor@linux.com |
| Silent Service II | 海军游戏 | jvdbergh@wins.be |
| thunderByte scan | 杀毒软件 | jvdbergh@wins.be |
| Ventura Publisher 3.0 | 桌面出版 | niemann@swt.ruhr-bochum.de |
| wildunix | | |
| wild cards | 通配符 | miguel@pinon.ccu.uniovies |
| Windows 3.1 | | juphoff@n..vt.edu |

在 DOSEMU 下运行程序有几个问题，因为它们是在模拟 DOS 和底层机器，而不是运行 DOS。仿真会减慢系统。当你同时在其他终端运行其他 Linux 程序时，这种延迟会变得令人烦恼。在 DOSEMU 下视频更新也较慢。

# 在 Linux 下运行 Windows 程序

| 名称 | 功能 | 发布者 |
|---|---|---|
| 4D | 游戏 | jvdbergh@wins.be |
| Apple | 模拟器 | jvdbergh@wins.be |
| Borland C++ 3.1 | 编译器 | juphoff@n.rai.vt.edu |
| brief | 编辑器 | bchow@slip |
| Chuck Yeager | 飞行仿真 | jvdbergh@wins.be |
| CIVILIZATION | 游戏 | miguel@pinon.ccu.uniovies |

## 表 5.10 续

| 名称 | 功能 | 发布者 |
|---|---|---|
| DesqView 2.51 | 界面 | hsw1@papa.atlas.com |
| doom | 游戏 | rideau@clipper.ens.fr |
| dpms | 压缩文件系统 | | |
| QBASIC/EDIT | 编辑器 | bchow@slip |
| NORTON UTILITIES 7.0 | 磁盘工具 | rideau@clipper.ens.fr |
| Quattro Pro 4.0 | 表格软件 | jwest@okstate.edu |
| Raptor | 游戏 | ensor@linux.com |
| Silent Service II | 海军游戏 | jvdbergh@wins.be |
| thunderByte scan | 杀毒软件 | jvdbergh@wins.be |
| Ventura Publisher 3.0 | 桌面出版 | niemann@swt.ruhr-bochum.de |
| wildunix | 通配符 | miguel@pinon.ccu.uniovies |
| Windows 3.1 | | juphoff@n.rai.vt.edu |

在 DOSEMU 下运行程序有几个问题，因为它们是在模拟 DOS 和底层机器，而不是运行 DOS。仿真会减慢系统。当你同时在其他终端运行其他 Linux 程序时，这种延迟会变得令人烦恼。在 DOSEMU 下视频更新也较慢。

# 在 Linux 下运行 Windows 程序

| 名称 | 功能 | 发布者 |
|---|---|---|
| 4D | 游戏 | jvdbergh@wins.be |
| Apple | 模拟器 | jvdbergh@wins.be |
| Borland C++ 3.1 | 编译器 | juphoff@n.rai.vt.edu |
| brief | 编辑器 | bchow@slip |
| Chuck Yeager | 飞行仿真 | jvdbergh@wins.be |
| CIVILIZATION | 游戏 | miguel@pinon.ccu.uniovies |

安装 Wine 与安装 DOSEMU 非常相似，不同之处你可以将源 tar 包放在任何地方。使用 `tar` 命令在目录中解压文件，如下所示：

```
