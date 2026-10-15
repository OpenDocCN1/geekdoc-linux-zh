
# 版本列表

- 3.9 `i86,x86-GA` 3.9 2.4.21-50 2007年7月26日 2007年6月15日 41
- 4.0 `i86,x86-GA,various` 4.0 2.6.9-5 2005年3月9日 2005年2月14日 23
- 4.1 `i86,x86-GA,CA,s390` 4.1 2.6.9-11 2005年6月12日 2005年8月1 4
- 4.2 `i386,x86-GA,IA,s390x,alpha` 4.2 2.6.9-22 2005年10月13日 2005年10月5日 8
- 4.3 `i386,x86-GA,IA,s390,s390x` 4.3 2.6.9-34 2006年3月21日 2006年3月12日 9
- 4.4 `i386,x86-GA` 4.4 2.6.9-42 2006年8月30日 2006年8月10日 20
- 4.5 `i386,x86-GA,IA` 4.5 5.2.6-55 2007年5月17日 2007年5月1日 16
- 4.6 `i386,x86-GA,IA,Alpha,s390x,PowerPC(beta), SPARC (beta)` 4.6 2.6.9-67 2006年12月16日 2007年11月17日 30
- 4.7 `i386,x86-GA` 4.7 2.6.9-78 2008年9月13日 2008年7月24日 51
- 4.8 `i386,x86-GA` 4.8 2.6.9-89 2009年8月21日 2009年5月18日 95
- 4.9 `i386,x86-GA` 4.9 2.6.9-100 2011年3月21日 2011年2月14日 14
- 5.0 `i386,x86-GA` 5.0 2.6.18-52 2007年4月12日 2007年3月14日 28
- 5.1 `i386,x86-GA` 5.1 2.6.18-53 2007年12月2日 2007年11月7日 25
- 5.2 `i386,x86-GA` 5.2 2.6.18-92 2001年6月24日 2008年5月21日 34
- 5.3 `i386,x86-GA` 5.3 2.6.18-128 2009年3月31日 2009年1月20日 69
- 5.4 `i386,x86-GA` 5.4 2.6.18-164 2009年10月21日 2009年9月2日 49
- 5.5 `i386,x86-GA` 5.5 2.6.18-194 2010年5月19日 2010年3月10日 44
- 5.6 `i386,x86-GA` 5.6 2.6.18-238 2011年4月8日 2011年1月11日 85
- 5.7 `i386,x86-GA` 5.7 2.6.18-274 2011年9月13日 2011年7月21日 54
- 5.8 `i386,x86-GA` 5.8 2.6.18-308 2012年3月7日 2012年2月21日 15
- 5.9 `i386,x86-GA` 5.9 2.6.18-348 2013年1月17日 2013年7月7日 10
- 5.10 `i386,x86-GA` 5.10 2.6.31-371 2013年10月19日 2013年9月30日 19
- 6.0 `i386,x86-GA` 6.0 2.6.32-71 2011年7月11日 2010年11月10日 242
- 6.1 `i386,x86-GA` 6.1 2.6.32-131 2011年12月9日 2011年5月19日 204
- 6.2 `i386,x86-GA` 6.2 2.6.32-220 2011年6月20日 60
- 6.3 `i386,x86-GA` 6.3 2.6.32-279 2012年7月9日 2012年6月21日 18
- 6.4 `i386,x86-GA` 6.4 2.6.32-358 2013年3月9日 2013年2月21日 15

## 目录服务 - LDAP 实现

在基于 `LDAP`/`X500` 的实现中：

- `Active Directory:` 微软用于 Windows 的现代目录，源自 `X500` 目录，为 `Exchange Server` 产生，首次随 `Windows 2000 Server` 发布，并由一系列版本的目录设施维护。
- `Novell edirectory:` 这是 `Novell` 的目录实现。它帮助许多设计，包括 `Microsoft Windows`、`NetWare`、`Linux` 和某些 `Unix` 变体，长期以来一直应用于用户管理、配置管理和代码管理。`EDirect` 开发为更广泛的身份管理的主要部分。它以前被称为 `Novell Directory Services`。
- `Red Hat Directory Server:` 红帽实现了一种目录设施，它是从 `AOL` 的网络安全解决方案组件获得的 `http://www.information.com/story/showArticle.html?articleID=4880390`，作为运行在红帽企业 `Linux` 之上的营利文章名为 `Red Hat Directory Server`，并且小组维护着 `389 Directory Server`。
- `eatives ViewDS Directory Server:` `ViewDS` `http://www.viewds.com` 身份和访问管理服务 - 授权服务 - 数据集成。`ViewDS`。

目录访问协议|`LDAP` 利用了 `OpenLDAP` 的修改版构造，旨在实现简单身份认证与安全层|`SASL` 以及 `Kerberos(协议)`|`Kerberos` 身份认证。它利用插件化设计，来与不同的 `LDAPv3` 目录工作，包含 `Active Directory` 和 `eDirectory` 等专属结果。

- `Apache Directory Server:` `Apache` 软件基金会提供名为 `Apache Directory Server`|`ApacheDS` 的目录设施。
- `Oracle Internet Directory:` `OID` 是 `Oracle` 公司的目录设施，它与 `LDAP 3` 变体兼容。
- `CA Directory:` `CA` 拥有预缓存机制，该机制可能包含应用于 `LDAP` 查找的所有功能，并存储恢复在查找结果中的所有功能。
- `Alcatel-Lucent Directory Server:` `CTIA 2009-4G` 服务创建奖获得者，增加了执行力、提升了可获取性并确认了效率。
- `Sun System Directory Server:` `Sun Microsystems` 提供名为 `OpenDS` 的目录设施；一种自 `Java` 诞生以来有效的目录设施，由 `Sun Microsystems` 赞助。
- `IBM Tivoli Directory Server:` 它是 `OpenLDAP` 旧版本的修改版构造。
- `DirX Directory` Server 属于 `Atos`（原西门子软件）。
- `Windows NT Directory Services (NTDS)`，后更名为 `Active Directory`，取代了原来的 `NT` 域配置。
- `critical Path, Inc.|Critical Path Directory Server`
- `OpenLDAP` 源自密歇根大学首次提到的 `LDAP` 效率（类似于 `Netscape/Red Hat/Fedora/Sun JSDS` 服务器），但经过了显著开发。它还提供了各种计算机设计，包括 `Unix` 和 `Unix` 衍生产品、`Linux`、`Windows`、`z/OS` 以及各种嵌入/实时设置。
- `Isode Limited:` 高性能、高可获取性的 `LDAP` 和 `X 500` 服务器。
- `Lotus Directory`
- `Nexor Directory`

有很多开源实现可以生成目录设施，包含 `OpenLDAP` 和 `Kerberos (协议)`|`Kerberos` 过程，以及作为具有 `Kerberos (协议)` 和 `LDAP` 后端的 `Windows` 域控制器的 `Samba` 代码。利用 `GOsa` 或 `Samba sent` 软件|`SWAT` 完成管理。

## Red Hat 集群套 - 历史

该套件可用范围：

- `Red Hat Enterprise Linux 2.1`
- `Red Hat Enterprise Linux 3.x, 4.x, 5.x` - 使用维护的全局文件系统 `v1.x` 作为文件系统
- `Red Hat Enterprise Linux 5.3` 及之后 - 使用全局文件系统 2
- `Red Hat Enterprise Linux 6.0` 及以后

填充代码是开源 `Piranha` 填充代码的分支。

## VMware vSphere - 历史

在 `VMware Infrastructure 3.5` 创作期间，`vSphere` 被设计为一套应用于 `VMware ESX/ESX/ESXi 4` 云计算的增强工具集。

`http://vsphere-land-com/news/vsphere-release-date.html` 文章
