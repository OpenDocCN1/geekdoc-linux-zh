

CIPE 可用于隧道技术，以创建虚拟专用网络（VPN）。低层加密的优势在于，它可以在通过 VPN 连接的两个网络之间透明地工作，而无需对应用软件进行任何更改。

摘自 CIPE 文档的摘要：

> IPSEC 标准定义了一组协议，这些协议（除其他用途外）可用于构建加密的 VPN。然而，IPSEC 是一个相当沉重且复杂的协议集，拥有众多选项，完整协议集的实现仍然很少被使用，并且一些问题（例如密钥管理）仍未得到完全解决。CIPE 采用了一种更简单的方法，其中许多可参数化的事项（例如实际使用的加密算法的选择）在安装时是固定的。这限制了灵活性，但允许实现简单（因此高效且易于调试）。

更多信息可参见 [http://www.inka.de/~bigred/devel/cipe.html](http://www.inka.de/~bigred/devel/cipe.html)。

与其他形式的密码学一样，由于出口限制，默认情况下不随内核分发。

## Kerberos

Kerberos 是由 MIT 雅典娜项目开发的身份验证系统。当用户登录时，Kerberos 验证该用户（使用密码），并向用户提供一种方法，以证明其身份给散布在网络中的其他服务器和主机。

随后，像 `rlogin` 这样的程序使用此身份验证，允许用户在登录到其他主机时无需输入密码（替代 `.rhosts` 文件）。这种身份验证方法也可由邮件系统使用，以确保邮件交付给正确的人，并保证发件人是其声称的身份。

Kerberos 及其随附的其他程序可防止用户让系统“伪装”相信他们是另一个人。不幸的是，安装 Kerberos 侵入性极强，需要修改或替换许多标准程序。

您可以通过查看 Kerberos FAQ（[http://www.cis.ohio-state.edu/hypertext/faq/usenet/kerberos-faq/general/faq.html](http://www.cis.ohio-state.edu/hypertext/faq/usenet/kerberos-faq/general/faq.html)）来获取更多关于 Kerberos 的信息，代码可在 [http://nii.isi.edu/info/kerberos](http://nii.isi.edu/info/kerberos) 找到。

来源：Stein, Jennifer G., Clifford Neuman, 和 Jeffrey L. Schiller. “Kerberos: An Authentication Service for Open Network Systems.” USENIX 会议论文集，德克萨斯州达拉斯，1998 年冬季。

Kerberos 不应是您提高主机安全性的第一步。它相当复杂，并且不像 ssh 那样被广泛使用。

## 影子密码（Shadow Passwords）

影子密码是一种保护您的加密密码信息不被普通用户获取的手段。通常，这些加密密码存储在 /etc/passwd 文件中，供所有人读取。任何人都可以运行密码猜测程序来尝试确定它们的值。相比之下，影子密码保存在 /etc/Shadow 中，只有特权用户可以读取。为了使用影子密码，您需要确保所有需要访问密码信息的实用工具都重新编译以支持它们。PAM（上文提到）也允许您直接插入影子模块；它不需要重新编译可执行文件。如有必要，您可以参考 Shadow-Password HOWTO 获取更多信息。它位于 [http://metalab.unc.edu/LDP/HOWTO/Shadow-Password-HOWTO.html](http://metalab.unc.edu/LDP/HOWTO/Shadow-Password-HOWTO.html)。现在它已经相当过时，且对于支持 PAM 的发行版来说并非必需。

## Crack 和 John the Ripper

如果由于某种原因您的 passwd 程序没有强制执行难以猜测的密码，您可能希望运行密码破解程序，以确保用户的密码是安全的。

密码破解程序基于一个简单的原理：它们尝试字典中的每个单词，以及这些单词的变体，对每个进行加密并与您的加密密码进行检查。如果匹配成功，它们就知道您的密码是什么。

市面上有许多此类程序——其中最著名的是 Crack 和 John the Ripper（[http://www.false.com/security/jown/index.html](http://www.false.com/security/john/index.html)）。它们会占用大量您的 CPU 时间，但通过先自行运行并通知拥有弱密码的用户，您应该能够判断攻击者是否可以使用这些程序入侵。请注意，攻击者首先需要利用其他漏洞才能读取您的 `/etc/passwd` 文件，但这种漏洞比您想象的更常见。

因为安全性仅取决于最不安全的主机，所以值得一提的是，如果您的网络上有任何 Windows 机器，您应该查看 *L0ph4Crack*，这是 Windows 版本的 Crack 实现。它可从 [http://www.10pt.com](http://www.10pt.com) 获取。

## CFS—密码文件系统 和 TCFS—透明密码文件系统

CFS 是一种加密整个目录树并允许用户在其上存储加密文件的方法。它使用在本地机器上运行的 NFS 服务器。RPM 包可在 [http://www.replay.com/redhat/](http://www.replay.com/redhat/) 找到，关于其工作原理的更多信息在 [ftp://ftp.research.att.com/dist/mab/](ftp://ftp.research.att.com/dist/mab/)。

TCFS 通过增加与文件系统的集成度来改进 CFS，使用户能够透明地感知文件系统被加密。更多信息可参见 [http://edu-gw.dia.unisa.it/tcfs/](http://edu-gw.dia.unisa.it/tcfs/)。

它也不必应用于整个文件系统。它同样适用于目录树。

## X11、SVGA 和显示安全

以下三个部分讨论视频安全的组成部分。

### X11

保护您的图形显示器以防止攻击者获取您输入的密码、读取您屏幕上的文档或信息，甚至利用漏洞获取 root 访问权限，这一点至关重要。通过网络运行远程 X 应用也可能充满危险，允许窃听者查看您与远程系统的所有交互。

X 具有多种访问控制机制。最简单的是基于主机的：您使用 *xhost* 来指定哪些主机可以访问您的显示器。这安全性极低，因为如果有人可以访问您的机器，他们可以使用 *xhost + their machine* 轻松进入。

此外，如果您必须允许来自不可信机器的访问，那里任何人都可以破坏您的显示器。

使用 xdm（X 显示管理器）登录时，您会得到一种更好的访问方法：MIT-MAGIC-COOKIE-1。会生成一个 128 位的 cookie 并存储在您的 .Xauthority 文件中。如果您需要允许远程机器访问您的显示器，您可以使用 xauth 命令和 .Xauthority 文件中的信息来仅为该连接提供访问权限。请参阅 Remote-X-Apps 小型 HOWTO，位于 [http://metalab.unc.edu/LDP/HOWTO/mini/Remote-X-Apps.html](http://metalab.unc.edu/LDP/HOWTO/mini/Remote-X-Apps.html)。

您还可以使用 ssh 来允许安全的 X 连接。其优势在于对最终用户也是透明的，并且意味着没有未加密的数据在网络上传输（参见章节“ssh [Secure Shell] and stlnter”）。

请参阅 Xsecurity 手册页以获取更多关于 X 安全的信息。稳妥的做法是使用 xdm 登录到控制台，然后使用 ssh 连接到您希望运行 X 程序的远程站点。

### SVGA

SVGAlib 程序通常是 SUID-root，以便访问您 Linux 机器的所有视频硬件。这使得它们非常危险。如果它们崩溃，您通常需要重新启动机器才能恢复可用的控制台。确保您运行的任何 SVGA 程序都是真实的，并且至少可以在某种程度上被信任。更好一点，根本不要运行它们。

### GGI（通用图形接口项目）

Linux GGI 项目试图解决 Linux 视频接口的几个问题。GGI 将把一小部分视频代码移入 Linux 内核，然后控制对视频系统的访问。这意味着 GGI 将能够随时将您的控制台恢复到已知良好的状态。它们还将允许使用安全注意键，因此您可以确定没有木马登录程序在您的控制台上运行（参见 [http://synergy.caltech.edu/~ggi/](http://synergy.caltech.edu/~ggi/)）。

## 内核安全（KERNEL SECURITY）

这是对与安全性相关的内核配置选项的描述，以及解释它们的作用和使用方法。

