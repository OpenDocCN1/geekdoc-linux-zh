
[content]

# 使用 telnet 和 ftp

```
-rw-r-xr-x 1 johnson archiviis 43442 May 24 1991 colorfinder.hqx
226 Transfer complete.
remote:colorfinder.hqx
71 bytes received in 0 seconds (0.069 Kbytes/s)
ftp get colorfinder.hqx
200 PORT command successful.
150 Opening BINARY data connection for colorfinder.hqx (43442 bytes).
228 Transfer complete.
local:colorfinder.hqx remote:colorfinder.hqx
43442 bytes received in 2.9 seconds (20 Kbytes/s)
ftp by
221 CUL8.
%
```

现在我已经处于命令提示符界面，可以使用它来确认我已收到了 `colorfinder.hqx` 和 `login.netcom` 文件：

+   % Is
Archives/ bin/ keyline.pie sample3
Infolold/ buckaroo login.netcom src/
Mail/ buckaroo.conf news listing
News/ cheryl paper.article temp/
OWL/ colorfinder.hqx sample temp/
awscript sample dickens.not2 who.is

FTP 系统是从互联网获取信息的极佳方式。许多家庭系统也通过匿名 FTP 提供各种服务。表 23.2 列出了其中最有趣的几个。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_497_0.png)

# 表 23.2 一些有趣的 FTP 归档。

| 站点 | 机构及可用信息 |
| --- | --- |
| aenas.mit.edu | 麻省理工学院。自由软件基金会站点。GNU EMACS |
| aisun.ai.uga.edu | 乔治亚大学。文件：LISP, PROLOG, 自然语言处理, MS-DOS 实用 |
| archive.nevada.edu | 内华达大学。文件：美国宪法及支持性文件，宗教文本，圣经 |
| brownm.brown.edu | 布朗大学。文件：Mac |
| cc.sfu.ca | 西哥华大学。文件：MS-DOS, Mac |
| clax1.cl.msu.edu | 密歇根州立大学。文件：MS Windows |
| cs.rice.edu | 莱斯大学。文件：Sun-Spots, Amiga, isfell |
| cscihp.ecst.csuchico.edu | 加州州立大学奇科分校。文件：在线化学手册 |
| cu.nih.gov | 美国国立健康研究院 |
| deja-vu.aiss.uiuc.edu | 伊利诺伊大学香槟-厄巴纳纳分校。文件：Rush Limbaugh 转录，蒙蒂派森，幽默，歌词，电影剧本，都市传说 |
| f.ms.uky.edu | 肯塔基大学。文件：Mac, MS-DOS, UNIX, Amiga, NeXT, 386BSD, AppleII, GNU, RFCs，各种 Usernet 归档 |
| ftp.apple.com | 苹果计算机。文件：Apple (Mac, IIs) 产品信息，软件，开发者支持 |
| ftp.cica.indiana.edu | 印第安纳大学。文件：Mac, MS-DOS, NEXT 更新，MS Windows 3.x 归档 |
| ftp.csc.liv.ac.uk | 利物浦大学计算机科学系。文件：到 HP-UX 机器的端口（特别是 700 系列），包括 X11R4 客户端，GNU，娱乐软件，文本编辑器，系统管理员 |
| ftp.eff.org | 电子边界基金会 |
| gatekeeper.dec.com | 数字设备公司，加利福尼亚州帕洛托。文件：X11, 配方，cron, 地图, Modula-3 |
| hobicat.cs.caltech.edu | 加州理工学院。文件：GNU（自由软件基金会） |
| hpcvaaz.cv.hp.com | 惠尔士-帕科，俄勒冈州科瓦利斯。文件：Motif，马里兰大学归档。文件：政府相关，书籍，经济学，MS-DOS, 小说，Mac |
| midgard.ucsc.edu | 加州大学圣塔克鲁兹分校。文件：amoeba, 美国宪法 |
| nnsc.nsf.net | 国家科学基金会网络。文件：网络信息，互联网资源指南 |
| nsdca.gsfc.nasa.gov | 美国航空航天局。哈哈勃太空望远镜图像 |
| sciences.sdsu.edu | 圣地亚哥州立大学。文件：声音 |
| sparkfyks.erg.ri.com | SRI 国际公司文件：提高你的 UNIX 系统安全性 |
| tesla.ee.cornell.edu | 康奈尔大学。文件：tsch |
| vax.ftp.com | FTP 软件。文件：FTP 相关程序 |
| watsun.cc.columbia.edu | 哥伦比亚大学。文件：kermit |
| wsmr-simtel2.army.mil | 美国陆军白沙导弹场。文件：MS-DOS, UNIX, CPM, Mac |

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_498_0.png)

# 使用 telnet 和 ftp

毫无疑问，ftp 的界面确实很笨拙，但正如你在本书的最后一个小时节中中学到的，有几个不同的程序尝试解决这个问题。

没有办法完全涵盖互联网上提供的所有信息，因此如果你对这些可能性感到兴奋，我强烈建议你获取由 Mark Gibbs 和 Richard Smith 编写的《导航互联网》（Navigating the Internet）一书。它是对互联网上许多服务的极佳介绍，包括 gopher、archie、万维网、telnet 和 ftp。不过，在本节一小时课程内未涵盖的内容将在本书的最后一个小时节中展示；因此，你至少将看到一些最重要的与互联网相关的命令。

# 任务 23.3：使用 archie 查找归档

如果你花点时间看上一个任务中的 FTP 归档列表，你就会意识到，仅仅在一个系统中获取文件列表可能都是一项艰性工作。计算机非常适合作为自己的导航助手，因为它们可以轻松处理大型复杂的数据库。

archie 系统是在加拿大的麦吉尔大学开发的。它是全球所有已注册 FTP 站点上可用文件和目录的巨大数据库。这非常惊人：超过 250 万个不同的文件。

（此处省略了大量重复的 OCR 噪声文本）

archie 系统：
- -a：考虑大小写敏感性
- -e：强制精确匹配
- -l：列出所有服务器
- -p：强制大写或小写
- -r：搜索正则表达式

