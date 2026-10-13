
幸运的是，这正是 shell 脚本大显身手的好地方。为了实现这一目标，我们只需扩展之前编写的 enabled 脚本，根据系统配置来检查 inetd 或 xinetd：

```sh
# cat enabled
#!/bin/sh

# enabled - show what services are enabled with inetd and xinetd,
# if they're available on the system.

iconf="/etc/inetd.conf"
xconf="/etc/xinetd.conf"
xdir="/etc/xinetd.d"

if [ -r $iconf ] ; then
 echo "Services enabled in $iconf are:"
 grep -v "#" $iconf | awk '{print $1}'
 echo
 if [ "`ps -aux | grep inetd | egrep -vE '(xinet|grep)'`" == "" ] ; then
 echo "*** warning: inetd does not appear to be running"
 fi
fi

if [ -r $xconf ] ; then
 # don't need to look in xinetd.conf, just know it exists
 echo "Services enabled in $xdir are:"

 for service in $xdir/*
 do
 if [ "`grep disable $service | grep 'yes'" == "" ] ; then
 echo -n " "
 basename $service
 fi
 done

 if [ "`ps -aux | grep xinetd | grep -v 'grep'" == "" ] ; then
 echo "*** warning: xinetd does not appear to be running"
 fi
fi

exit 0
```

这个脚本现在可以清楚地显示 xinetd 下启用了哪些服务，以及禁用了哪些服务：

```
# enabled
Services enabled in /etc/xinetd.d are:
sgi_fam
```

稍加探查，即可确认 sgi_fam 的真实身份：

```
# grep server /etc/xinetd.d/sgi_fam
server	= /usr/bin/fam

# man -k fam
fam (1m) - file alteration monitor
fam (3x) - File Alteration Monitor (FAM) library routines
grolj4 (1) - groff driver for HP Laserjet 4 family
```

显然，这是一个文件修改监视器。我们可能希望启用它，也可能不希望，但除此之外，可以确认该服务器上没有运行其他多余的服务，这令人放心。

xinetd 及其配置文件还有更多内容，尤其是在可以指定的众多参数方面。如果你的系统运行着 xinetd，强烈建议你留出 30 分钟时间，通读 xinetd 和 xinetd.conf 文件，了解如何精确控制系统中的这一重要功能。

## 示例：启用 ftp

在 Unix 的世界里，ftp 一直是最有用的命令之一。尽管它绝算不上美观——坊间的玩笑话是它总是处于调试模式——但它是计算机系统之间传输文件的一种直接了当的方式。

随着 X Window 系统以及 Mac 和 Windows 计算机上出现了美观的 FTP 客户端界面，使用这种机制已经大大简化了。

那么，如何在服务器上启用 ftp 呢？

### 任务 19.4：启用 ftp（以及你可能不想启用它的原因）

承认吧，这个奇怪的章节标题勾起了你的兴趣。在我解释为什么你可能不想启用 ftp 之前，先来看看启用基本访问所需的步骤。

1. 要仅启用有效账户访问（例如，允许那些在系统上有账户并知道相应账户密码的用户访问），只需在 /etc/inetd.conf 文件中启用 ftpd，或者在 /etc/xinetd.d 目录下的 ftp（或许还有 wu-ftpd）文件中启用即可。

   在启用 ftp 之前快速测试一下，显示它处于关闭状态：

   ```
   # ftp localhost
   ftp: connect: Connection refused
   ftp> quit
   ```

   一旦在 inetd.conf 文件中取消对该行的注释（或者在 xinetd 下将 enable 选项设置为 yes，这当然也会将下面的第一行改为重启 xinetd 所需的语句），然后快速重新读取配置文件。

   ```
   # kill -HUP `cat /var/run/inetd.pid`
   # ftp localhost
   Connected to localhost.
   220 dsl-132.dsidesigns.net FTP server (Version 6.00LS) ready.
   Name (localhost:taylor): ftp
   530 User ftp unknown.
   ftp: Login failed.
   ftp> quit
   221 Goodbye.
   #
   ```

   如果你运行的是 Mac OS X 系统，请注意，启用 FTP 最简单的方法是在共享控制面板（可从“Apple”>“系统偏好设置”访问）中勾选“启用 FTP 访问”复选框。不过，你仍然需要手动配置匿名 FTP。

2. 注意，尽管 ftp 程序现在会监听连接并显示常规的 ftpd 对话框，但匿名 FTP 访问仍然被禁用。（连接到匿名 FTP 服务器的标准方式是以 ftp 身份登录，并使用你的电子邮件地址作为密码。）

   ![](img/5ced0c78d748bd190e9027e5549a3622_402_0.png)

   > 匿名 FTP 服务允许互联网上的用户连接到你的服务器，四处翻找、下载文件，如果权限设置实在不当，还能上传他们自己的文件。从安全角度来看，这是一个典型的混合体。一方面，向系统提供匿名访问是友好且便捷的；但另一方面，这也非常危险，因为许多破解者会四处寻找可利用的 FTP 服务器。

   要启用匿名 FTP 服务，你需要创建一些特殊目录，并在其中放置特定文件和 Unix 可执行二进制文件的副本。其思路是创建一个文件系统的封闭子集，其中包含关键文件（ls 和一个精简后的 /etc/passwd），然后将匿名 FTP 用户困在该区域内。

   ![](img/5ced0c78d748bd190e9027e5549a3622_402_1.png)

   > 如果你运行的是 Red Hat Linux 或其他与 RPM 兼容的 Unix 系统（更多细节请参阅第 8 小时），最好的办法是直接安装 anonftp 包，而不是一步步手动操作。

   第一步必要操作是创建 ftp 用户账户。将该账户的主目录设置为 /bin/false 或另一个能阻止任何人将其用于 telnet 或其他会话的程序。你可以将密码设置为几乎任何值，因为 ftp 程序本身永远不会检查它（记住，按照惯例，匿名 ftp 用户会使用他们的电子邮件地址作为密码）。

   创建该账户后，进入其主目录并键入以下命令：

   ```
   # cd ~ftp
   # mkdir bin etc lib pub
   # chown root.root bin etc lib
   # chown root.ftp pub
   # chmod 111 bin etc
   # chmod 755 lib
   # chmod 2755 pub
   ```

   这会在 ftp 主目录中创建一个目录结构，镜像标准 Unix 文件系统的某些核心部分。

   下一步是将特定文件复制到 lib 和 bin 目录中。不过，这会因 Unix 的不同版本而异：Red Hat Linux 由于其动态加载器架构，需要将库放在 lib 中，而其他 Unix 版本可能不需要 lib 中有任何内容。由于这是一个非常关键的配置问题，请咨询你的供应商，获取针对你的操作系统版本的具体指南。

   让我们继续 Red Hat Linux 的配置：

   ```
   # cp /lib/{ld-2.1.1,libc-2.1.1,libnsl-2.1.1,libnss_files-2.1.1}.so ~ftp/lib
   # chmod 755 ~ftp/lib/*
   # cp /usr/bin/compress ~ftp/bin
   # cp /bin/{cpio,gzip,ls,sh,tar} ~ftp/bin
   # chmod 111 ~ftp/bin/*
   ```

   还需要一些符号链接：

   ```
   # cd ~ftp/lib
   # ln -s ld-2* ld-linux.so.2
   # ln -s libc* libc.so.6
   # ln -s libnsl* libnsl.so.1
   # ln -s libnss* libnss_files.so.2
   # cd ../bin
   # ln -s gzip zcat
   ```

   现在，Red Hat Linux 配置的一切都应该就绪了。

   ![](img/5ced0c78d748bd190e9027e5549a3622_403_0.png)

   > 注意 {a,b,c} 这种巧妙的 shell 模式匹配符号，它会生成三个文件名：a、b 和 c。这是一个很棒的快捷方式。

   如果你使用不同的 Unix，安装过程可能会更像这样：

   ```
   # cp /bin/ls ~ftp/bin
   # chmod 111 ~ftp/bin/ls
   ```

   是不是简单多了？

3. 最后一步需要在 ~ftp/etc 中创建一个虚拟的 passwd 和 group 文件。我们可以复制现有文件，但更好的做法是创建一个非常精简的新文件，如下所示：

   ```
   # cat ~ftp/etc/passwd
   root:*::0:0::
   bin:*::1:1::
   operator:*::11:0::
   ftp:*::14:50::
   nobody:*::99:99::
   # cat ~ftp/etc/group
   root::0:
   bin::1:
   daemon::2:
   sys::3:
   adm::4:
   ftp::50:
   ```

   完成所有这些更改后，用户现在就可以匿名登录到 ftp 服务器了：

   ```
   # ftp localhost
   Connected to localhost (127.0.0.1).
   220 staging.intuitive.com FTP server (Version wu-2.6.1-18) ready.
   Name (localhost:taylor): ftp
   331 Guest login ok, send your complete e-mail address as password.
   Password:
   230 Guest login ok, access restrictions apply.
   Remote system type is UNIX.
   Using binary mode to transfer files.
   ftp>
   ```

4. 现在该谈谈安全性了，以及为什么你可能根本不想运行 FTP，更不用说匿名 FTP 了。

   首先，想象一下如果你不小心让 pub 目录对所有人可写会怎样。用不了多久，某个破解者就会偶然发现它并创建一个子目录，然后你就会发现你的系统被用作非法软件（行话称为“warez”）甚至色情内容的存储仓库。

   更糟糕的是，ftpd 守护进程是试图利用来闯入系统的热门应用程序（例如，多年前臭名昭著的互联网蠕虫就是通过 ftpd 撬开远程系统大门的），因此即使只是运行它，也会让你面临危险活动。

   也许 ftp 最致命的方面——这也是 telnet 同样具有的特点——是它不会对与客户端计算机共享的任何信息进行加密。账户名、密码、数据——全都是明文。这意味着坏人可以相当容易地用数据包分析器或类似工具从网络数据流中截获账户和密码对。
