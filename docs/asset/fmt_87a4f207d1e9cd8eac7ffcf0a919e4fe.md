
有关更多可能性，请参阅 `freebsd-update.conf(5)`。

#### 运行 `freebsd-update(8)`

使用二进制更新升级系统有两个阶段：下载更新和应用它们。如果你应用补丁而不是跨越主要版本升级，过程看起来略有不同。

如果你使用的是 ZFS，在升级或打补丁前务必创建一个新的引导环境！

##### 更新到最新的补丁级别

要下载所选发行版的最新补丁，运行 `freebsd-update fetch`。这里，我将一台 FreeBSD 11.0 主机更新到最新的补丁级别。

```
###### freebsd-update fetch
```

你将看到程序正在查找补丁的下载源，比较这些下载源的加密密钥，并最终将补丁下载到 `/var/db/freebsd-update`。检查系统可能需要几分钟时间，具体取决于你的存储速度。

偶尔，你会看到类似这样的消息：

##### 更新发布版本

作为更新到 `11.0-RELEASE-p12` 的一部分，以下文件将被移除：

- `/boot/kernel/hv_ata_pci_dsenengage.ko`
- `/usr/share/zoneinfo/America/Santa_Isabel`
- `/usr/share/zoneinfo/Asia/Rangoon`

我们正在将一个 `.0` 发布版本（即主要 FreeBSD 发布版本的第一版）直接更新到 `11.0-RELEASE-p12`，因此累积了一些补丁。为什么这样的补丁集会以移除文件开始？

时区文件非常直接明了。从 FreeBSD 11.0 发布到现在，圣伊莎贝尔 [2] 和仰光 [3] 改变了它们的时区。不幸的是，国家并不会协调它们的时区与 FreeBSD 的发布版本。从系统中移除这些时区可以简化这些国家系统管理员的生活，也不会对我们其他人造成伤害。

但他们也在移除一个内核模块 [1]。为什么会这样？在 FreeBSD 邮件列表上进行一点调研表明，这个模块本不应该随 11.0 一起发布，而且你 `真的` 不应该使用它。这种变更很罕见，但可能在主要版本发布后发生。

然后你会看到作为此补丁集一部分添加的文件（如果有的话）。

作为更新到 `11.0-RELEASE-p12` 的一部分，将添加以下文件：

- `/usr/share/zoneinfo/Asia/Barnaul`
- `/usr/share/zoneinfo/Asia/Famagusta`
- `/usr/share/zoneinfo/Asia/Toms`
- `-- snip --`

看起来仰光的系统管理员在这个夏天非常忙碌。

几乎所有的补丁都会修改系统中现有的文件。接下来你会看到那些文件。

作为更新到 `11.0-RELEASE-p12` 的一部分，将更新以下文件：

- `/bin/freebsd-version`
- `/boot/gptboot`
- `/boot/gptzfsboot`
- `/boot/kernel/cam.ko`
- `/boot/kernel/hv_storvsc.ko`
- `-- snip --`

如果你的发布版本即将达到生命周期结束（End of Life），你会看到如下通知：

```
WARNING: FreeBSD 11.0-RELEASE-p1 is approaching its End-of-Life date.
It is strongly recommended that you upgrade to a newer
release within the next 1 month.
```

如果发布版本已经超过了生命周期结束，通知会变得更加……强调。

要安装已下载的文件，请运行 `freebsd-update install`：

```
###### freebsd-update install
Installing updates... done.
```

如果更新需要更多步骤，你会在这里看到它们。重启你的系统，然后你会发现你正在运行最新的补丁级别。

##### 更新发布版本

这台 FreeBSD `11.0-p12` 机器将在一个月内达到生命周期结束？让我们使用 `freebsd-update upgrade` 更新它。使用 `-r` 标志指定目标发布版本。

```
###### freebsd-update -r 11.1-RELEASE upgrade
```

这部分最难的地方在于记得 `-RELEASE` 是版本号的一部分。

升级过程将检查你的系统并呈现其结论。

```
The following components of FreeBSD seem to be installed:
kernel/generic world/base world/lib32

The following components of FreeBSD do not seem to be installed:
kernel/generic-dbg world/base-dbg world/doc world/lib32-dbg

Does this look reasonable (y/n)? y
```

还记得安装过程吗，当时你选择了 FreeBSD 组件以在新主机上设置？`freebsd-update` 正在检查的就是这些。不过，你之前可能添加或移除了组件，所以要检查一下列表。如果看起来正确，按 `y` 继续。

更新过程将更仔细地审查系统，将所有现有文件与新发布版本进行比较，然后开始下载。

```
Fetching 10697 patches....10....20....30....40....50....60....70....80....90
```

去泡杯茶吧。根据你的主机带宽，你应该回来看到：

```
Applying patches...
```

你的茶可能太烫了。让它凉一会儿。

```
Fetching 236 files...
```

还有更多下载？没问题，享受你的茶，看着程序运行。

```
Attempting to automatically merge changes in files... done.
The following files will be removed as part of updating to 11.1-RELEASE-p1:
/usr/include/c++/v1/__undef__deallocate
/usr/include/c++/v1/tr1/__undef__deallocate
/usr/include/netinet/ip_ipsec.h
--snip--
```

你可以搜索邮件列表归档和 FreeBSD 源代码树来了解为什么这些文件被移除。

次要发布版本将包含从 `-current` 移植的新功能。这些功能可能涉及向系统中添加文件。

```
The following files will be added as part of updating to 11.1-RELEASE-p1:
/boot/kernel/amd_ecc_inject.ko
/boot/kernel/bytgpio.ko
/boot/kernel/cfiscsi.ko
/boot/kernel/cfunass.ko
--snip--
```

这些新功能不应干扰现有功能，但浏览列表可能会提供有趣的阅读材料。

升级应该会改变系统中几乎所有的文件，正如我们将在下文中看到的。

```
The following files will be updated as part of updating to 11.1-RELEASE-p1:
/.cshrc
/.profile
/COPYRIGHT
/bin/[
/bin/cat
--snip--
```

最终你会看到：

```
To install the downloaded upgrades, run "/usr/sbin/freebsd-update install".
```

谁有权忽视指令？

到目前为止，更新过程仅下载了文件并在临时暂存区进行了比较。操作系统尚未被触及。如果你感觉可以继续进行，请运行安装。

```
###### freebsd-update install
src component not installed, skipped
Installing updates...
Kernel updates have been installed. Please reboot and run
"/usr/sbin/freebsd-update install" again to finish installing updates.
```

为什么在更新的部分之间要重启？新的用户空间程序可能需要新的内核功能。安装一个无法工作的重启命令版本会导致需要给主机断电循环，这会在你的极客卡上留下一记令人尴尬的一拳。

```
###### reboot
```

一旦机器重新启动完成用户空间升级。

```
###### freebsd-update install
src component not installed, skipped
Installing updates...
Completing this upgrade requires removing old shared object files.
Please rebuild all installed 3rd party software (e.g., programs
installed from the ports tree) and then run "/usr/sbin/freebsd-update
install" again to finish installing updates.
```

这是什么疯狂的行为？

更新过程努力避免留下损坏的系统或功能失调的软件。如果 `freebsd-update` 移除了你的附加软件所需的旧版本共享库，该软件将无法运行。更新过程暂停，以便你有机会升级你的软件。

我们将在本章稍后讨论升级包和端口。沿着 `-stable` 分支的升级通常不需要移除旧的残留物。

最后一次运行 `freebsd-update` 将移除旧的共享库等。

```
###### freebsd-update install
```

你的升级现在完成了。正如进行任何广泛的系统维护时一样，最后再重启一次以验证一切是否干净启动。

##### 回滚更新

你以为升级会顺利。以前总是如此。但这次，你错了。新补丁与你的软件之间的一些微妙交互让你遭遇了困境。如果你正在使用引导环境（boot environments），现在是回滚到之前安装的时候了。如果你没有使用，请使用 `freebsd-update` 的 `rollback` 命令移除最近安装的升级。

```
###### freebsd-update rollback
Uninstalling updates... done.
```

回滚比安装补丁快得多。无需检查系统；`freebsd-update` 只是读取其先前操作的日志并撤销所有操作。

##### 安排二进制更新

最佳实践建议按照定期日程，在一致的时间下载和应用更新，例如在你的每月维护日。`freebsd-update` 程序包含对此特定支持，以避免每小时整点向下载服务器发出请求而淹没它们。`freebsd-update cron` 命令告诉系统在下一小时的随机时间点下载更新。将此命令放入 `/etc/crontab` 以在该一小时内下载更新。这有助于减少下载服务器的负载。当系统有更新时，你会收到电子邮件，这样你就可以方便地安排重启。

##### 优化和自定义 FreeBSD Update

关于 FreeBSD Update 的两个常见问题涉及 FreeBSD 的自定义构建和在本地分发更新。

许多人构建自己的 FreeBSD 版本用于内部使用。通常，这只是切除了各个部分的 FreeBSD 版本，但有些公司使用大量修改。如果你已从 FreeBSD 安装中删除文件，`freebsd-update(8)` 不会尝试修补它们。

类似地，许多公司喜欢拥有内部更新服务器用于补丁管理。FreeBSD Update 系统特别设计为与缓存 Web 代理配合工作。虽然所有文件都经过加密签名和验证，但它们通过纯 HTTP 传输，以便你的代理可以缓存它们。

##### 通过源代码升级

更新系统的另一种方式是从源代码构建它。FreeBSD 是 `自我托管` 的，意味着它包含构建 FreeBSD 所需的所有工具。你不需要安装任何编译器或开发工具包。你唯一需要从源代码构建新的 FreeBSD 的东西就是新的源代码。

当开发者发布 FreeBSD 的改进时，更改在全球范围内几分钟内即可获取。FreeBSD 主源代码服务器跟踪源代码、对该代码所做的所有更改以及这些更改的作者。开发者可以签入新代码，用户可以通过 `Subversion` (`SVN`) 签出最新版本。FreeBSD 有一个简单的 SVN 客户端 `svnlite(1)`，足以满足所有源代码操作需求。它是一个标准的 Subversion 客户端，未包含 `svn(1)` 支持的任何复杂选项。许多人发现 `svnlite(1)` 对于他们所有非 FreeBSD 的 Subversion 需求都完全足够。

### CSUP、CVSUP、CVS、SUP 和 CTM？

遗憾的是，互联网上的文档往往在毫无逻辑的情况下长期存续，并在最不恰当的时刻制造混乱。过时的 FreeBSD 文档和第三方教程可能会提及使用名为 `CVS` 或 `CVSup` 的工具来更新源代码。这些工具已在 2013 年被取代。任何提及这些程序的地方都表明你正在阅读旧文档。如果你看到关于 CTM 的提及，说明你阅读的是比 CVS 更早的文档。

从源码升级需要控制台访问权限。虽然你并非总是需要它，但在恢复失败的构建时，可能需要你在键盘上进行干预。在安装你自行构建的操作系统版本之前，请测试你的串行控制台、Java 应用程序或 IPMI 控制台。根据我的经验，唯一需要控制台访问权限的升级，恰恰是那些我没有控制台访问权限的情况。

#### 哪些源代码？

每个 FreeBSD 版本都附带了用于构建你所安装系统的源代码。如果安装系统时你未选择安装源代码，你可以在安装介质中的 `/usr/freebsd-dist/src.txz` 找到它。如果你已经安装了源代码，它位于 `/usr/src`。

不幸的是，这个版本的源代码缺乏构建 FreeBSD 所需的版本控制标签。它仅供参考。你需要使用 `svnlite(1)` 下载一个保留这些标签的代码版本。

`/usr/src` 中的源代码副本适合用于构建 FreeBSD 吗？问 `svnlite(1)`。

```
##### svnlite info /usr/src
svn: E155007: '/usr/src' is not a working copy
```

“不是工作副本”的错误意味着这里的任何源代码都无法与 Subversion 配合使用。

获取源代码的 `svnlite(1)` 命令如下所示。

```
##### svnlite checkout \*svn.freebsd.org/@repository/@branch @locadir
```

`Mirror` 是一个 FreeBSD Subversion 镜像。`svn.FreeBSD.org` 镜像是一个地理位置路由的别名，指向最近的 Subversion 镜像。

`Repository` 是你正在处理的代码组。你可以在 `https://svnweb.FreeBSD.org/` 获取当前仓库的完整列表。主要项目仓库包括：`base`（用于操作系统）、`doc`（用于文档）和 `ports`（用于 Ports Collection）。

`Branch` 是你想要的 FreeBSD 版本。为了获取最新的、指尖笨拙的 `current` 版本，请使用 `head`。要获取稳定版本，请使用 `stable/` 后跟主要发行版本号。FreeBSD `12-stable` 即 `stable/12`。要获取发行版加上当前所有补丁，请使用 `releng/` 后跟发行版编号。完全修补的 FreeBSD `12.2` 位于 `releng/12.2`。

如果你难以确定需要哪个分支，不妨浏览 `https://svnweb.freebsd.org/`。分支字面上告诉 `svnlite(1)` 从该站点抓取哪个子目录。

最后，`locadir` 是我希望存放源代码的本地目录。

这台主机运行的是 FreeBSD `11.1`。我想要冒险一点，升级到 FreeBSD `11-stable`。以下是我的操作方法：

```
##### svnlite checkout https://svn0.us-east.FreeBSD.org/base/stable/11 /usr/src/

Error validating server certificate for 'https://svn0.us-east.freebsd.org:443':
  - The certificate is not issued by a trusted authority. Use the
    fingerprint to validate the certificate manually!
Certificate information:
  - Hostname: svn0.freebsd.org
  - Valid: from Jul 29 22:01:21 2013 GMT until Dec 13 22:01:21 2040 GMT
  - Issuer: svn0.freebsd.org, clusteradm, FreeBSD.org, CA,
    US(clusteradm@freebsd.org)
  - Fingerprint: 1C:BD:85:95:11:9F:EB:75:A5:4B:C8:A3:FE:08:E4:02:73:06:1E:61
(R)eject, accept (t)emporarily or accept (p)ermanently? p
```

这是什么新的疯狂举动？我们试图获取 FreeBSD 源代码，结果却遇到了证书错误？

将显示的证书指纹与 `FreeBSD.org` 网站上的服务器指纹进行对比。如果匹配，请输入 `p` 永久接受证书。源代码文件的文件名将从你的终端流过。

`svnlite(1)` 完成后，查看一下 `/usr/src`。
