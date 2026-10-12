
也许在询问你可以从哪里获取 RPM 之前，先查看你的系统上是否已经安装了 RPM 会更好。如果你的系统上安装了 Red Hat Linux，那么它已经在那里了。但一定要在其他操作系统上检查一下：人们每天都在将 RPM 移植到不同的操作系统上，它可能正等着你呢。

这里有一种快速方法来查看你的系统上是否安装了 RPM：

```
% rpm - --version
RPM version 2.3
%
```

如果这个命令不起作用，可能是因为你的路径中没有包含 RPM 所在的目录。在断定 RPM 未安装之前，请先检查常规的二进制目录！

### F.1.1. FTP 站点

如果你无法在系统上找到 RPM，你将不得不通过 FTP 获取一份副本。只要 Red Hat Linux 存在的地方，几乎都能找到 RPM。虽然最明显的站点 `ftp.redhat.com` 肯定是一个选项，但它可能不是你的最佳选择。一方面，该站点可能非常繁忙。另一方面，除非你到互联网的连接靠近 Red Hat 位于北卡罗来纳州达勒姆（Durham）庞大的开发园区，否则附近很可能有一个离你更近的 FTP 站点。

以下是镜像 Red Hat 软件主 FTP 站点的站点列表。请注意，此列表经常变动，所以如果某个站点不再镜像 Red Hat 或已从这里列出的路径移开，请不要感到惊讶（最新的镜像站点列表始终可在 `ftp.redhat.com` 上的 `MIRRORS` 文件中找到）：

| FTP 站点 | 目录 |
| :--- | :--- |
| sunsite.doc.ic.ac.uk | `/packages/linux/redhat` |
| ftp.mp1.sb.mpg.de | `/pub/linux/mirror/ftp.redhat.com` |
| ftp.jate.u-szeged.hu | `/pub/linux/redhat` |
| ftp.ibp.fr | `/pub/linux/distributions/redhat` |
| ftp.gwdg.de | `/pub/linux/install/redhat` |
| ftp.msu.ru | `/pub/OS/linux/redhat` |
| ftp.sgg.ru | `/mirror/redhat` |
| sunsite.mff.cuni.cz | `/OS/linux/Distributions/Redhat` |
| ftp.ton.tut.fi | `/pub/linux/Redhat` |
| ftp.funet.fi | `/pub/linux/images/Redhat` |
| sunsite.icm.edu.pl | `/pub/linux/redhat` |
| ftp.arch.pwr.poznan.pl | `/mirror/linux/redhat` |
| ftp.rh.i.his | `/pub/linux/Redhat` |
| ftp.nvg.unit.no | `/pub/linux/redhat` |
| ftp.pk.edu.pl | `/pub/linux/redhat` |
| ftp.nlug.nl | `/pub/os/linux/distr/Redhat` |
| dutepp0.et.tudelft.nl | `/pub/Unix/Linux/distributions/redhat` |
| ftp.iol.ie | `/pub/Unix/Linux/distributions/Redhat` |
| sunsite.auc.dk | `/pub/os/linux/redhat` |
| ftp.tku.edu.tw | `/Unix/Linux/Redhat` |
| ftp.cs.us.es | `/pub/Linux/redhat` |
| ftp.is.co.za | `/linux/distributions/redhat` |
| ftp.dstc.edu.au | `/pub/linux-redhat` |
| ftp.lab.kdd.co.jp | `/OS/Linux/packages/redhat` |
| sunsite.ust.hk | `/pub/Linux/distributions/redhat` |
| ftp.sunsite.dcc.uchile.cl | `/pub/OS/linux/redhat` |
| ftp.interpath.net | `/pub/linux/redhat` |
| schlit.z.cae.wisc.edu | `/pub/Linux/Redhat` |
| ftp.wwwnet.net | `/LINUX/redhat` |
| ftp.engr.uark.edu | `/pub/linux/redhat` |
| ftp.infomagic.co.com | `/pub/mirrors/linux/Redhat` |
| ftp.wgs.com | `/pub/linux/redhat` |
| ftp.drcdrom.com | `/pub/Linux-redhat` |
| ftp.hkstar.com | `/pub/Linux/redhat` |
| ftp.pht.com | `/pub/linux/redhat` |
| linux.uks.indiana.edu | `/pub/linux/redhat` |
| ftp.uoknor.edu | `/linux/redhat` |
| ftp.cc.gatech.edu | `/pub/linux/distributions/redhat` |
| uiarohive.cso.uiuc.edu | `/pub/systems/linux/distributions/redhat` |
| ftp.caldera.com | `/pub/mirrors/redhat` |
| ftp.cms.uncwll.edu | `/linux/redhat` |
| ftp.wilmington.net | `/linux/redhat` |
| sunsite.unc.edu | `/pub/linux/distributions/redhat` |
| gatekeeper.dec.com | `/pub/linux/redhat` |
| ftp.rge.com | `/pub/systems/linux/redhat` |
| linuxwwww.db.erau.edu | `/pub/linux/distrib/redhat` |
| ftp.eit.com | `/pub/mirrors/redhat` |
| ftp.real-time.com | `/pub/redhat` |

Red Hat 软件还专门建立了一个用于 RPM 的 FTP 站点。它位于 `ftp.rpm.org`，包含所有当前和过去的 RPM 版本。

### F.1.2. 我需要哪些文件？

一旦你找到附近存有 RPM 的站点以及存放它的目录，你会发现各种文件，它们都以 `rpm` 开头。它们是什么？你需要哪些？以下是具有代表性的列表，以及每个文件的使用方式：
