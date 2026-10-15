
<sup>132</sup>(Offensive Security, 2019). https://www.exploit-db.com/searchsploit/

| Microsoft Windows - 'AfdJoinLeaf' 权限提升 | https://www.exploit-db.com/exploits/21844 |
| --- | --- |
| Microsoft Windows - 'afd.sys' 本地内核权限提升 | https://www.exploit-db.com/exploits/18755 |
| Microsoft Windows 7 (x64) - 'afd.sys' 危险文件句柄 | https://www.exploit-db.com/exploits/39525 |
| Microsoft Windows 7 (x86) - 'afd.sys' 危险文件句柄 | https://www.exploit-db.com/exploits/39446 |
| Microsoft Windows 7 内核 - 基于池的溢出 | https://www.exploit-db.com/exploits/42009 |
| Microsoft Windows XP - 'afd.sys' 本地内核权限提升 | https://www.exploit-db.com/exploits/17133 |
| Microsoft Windows XP/2003 - 'afd.sys' 权限提升 | https://www.exploit-db.com/exploits/6757 |
| Microsoft Windows XP/2003 - 'afd.sys' 权限提升 | https://www.exploit-db.com/exploits/18176 |

**列表 178 - 使用 searchsploit 搜索利用工具**

这是一个良好的开端，但我们需要修剪结果。目前，我们只关注利用工具的 URL，因此让我们使用 `grep` 搜索 "`http`" ，然后使用 `cut` 提取所需内容。我们将使用 "`|`" 作为字段分隔符，并提取第二个字段：

```
kali@kali:~$ searchsploit afd windows -w -t | grep http | cut -f 2 -d "|"

https://www.exploit-db.com/exploits/40564

https://www.exploit-db.com/exploits/21844

https://www.exploit-db.com/exploits/18755

https://www.exploit-db.com/exploits/39525

https://www.exploit-db.com/exploits/39446

https://www.exploit-db.com/exploits/42009

https://www.exploit-db.com/exploits/17133

https://www.exploit-db.com/exploits/18176

https://www.exploit-db.com/exploits/6757
```

**列表 179 - 从 searchsploit 的输出中提取 URL**

这看起来好一些了。现在我们已经有了每个利用工具的 URL，我们可以使用 Bash 循环来下载文件并将其保存为本地文件。然而，在此之前，我们注意到每个页面都有一个链接可以下载“原始”利用工具代码，而这正是我们真正想要的：

![](img/ec25e59d75726b7041242a56d3376832_127_0.png)

我们可以看到，每个原始页面（例如 `/exploits/40564`）都链接到一个原始利用工具（例如 `/raw/40564`）。凭借这一信息，我们运行 `sed`（`sed 's/exploits/raw/'`）来修改下载 URL，并将其插入一个 Bash 单行命令中，以下载利用工具的原始代码：

```
kali@kali:~$ for e in $(searchsploit afd windows -w -t | grep http | cut -f 2 -d " ");
do exp_name=$(echo $e | cut -d "/" -f 5) && url=$(echo $e | sed 's/exploits/raw/') &&
wget -q --no-check-certificate $url -O $exp_name; done
```

请注意使用 `for` 循环遍历我们获取的 SearchSploit URL。在循环内部，我们将 `exp_name` 设置为利用工具的“名称”（使用 `grep`、`cut` 和命令替换）。如果成功（`&&`），我们使用 `wget` 获取利用工具（在安静模式下且不检查证书），并以利用工具名称作为本地文件名保存下来。

一旦我们运行它，我们等待命令提示符，并使用 `file` 命令验证利用工具确实已下载，以确认这些文件是文本文件：

```
kali@kali:~$ ls -l

total 124

-rw-r--r--  1 root root   1363 Mar  7 19:52 17133

-rw-r--r--  1 root root  12215 Mar  7 19:52 18176

-rw-r--r--  1 root root   9698 Mar  7 19:52 18755

-rw-r--r--  1 root root  11590 Mar  7 19:52 21844

-rw-r--r--  1 root root  10575 Mar  7 19:52 39446

-rw-r--r--  1 root root  14193 Mar  7 19:52 39525

-rw-r--r--  1 root root  32674 Mar  7 19:52 40564

-rw-r--r--  1 root root  12643 Mar  7 19:52 42009

-rw-r--r--  1 root root    619 Mar  7 19:52 6757

kali@kali:~$ file 17133

17133: C source, ASCII text, with CRLF line terminators
```

我们可以检查每个利用工具，看到我们实际上确实获取了原始利用工具：

```
kali@kali:~$ cat 17133

/////////////////////////////////////////////////////

//

// Title: Microsoft Windows xp AFD.sys Local Kernel DoS Exploit

// Author: Lufeng Li of Neusoft Corporation

// Vendor: www.microsoft.com

// Vulnerable: Windows xp sp3

//

/////////////////////////////////////////////////////

#include <stdio.h>

#include <Winsock2.h>

#pragma comment (lib, "ws2_32.lib")

BYTE buff[]={

0xac,0xfd,0xd3,0x00,0x01,0x00,0x00,0x00,0x00,0x00,

0x00,0x00,0x20,0x00,0x00,0x00,0x08,0xfd,0xd3,0x00,

0x00,0xfd,0x00,0x08,0xfd,0xd3,0x00,0xc4,0xfd,

0xd3,0x00,0xcc,0xfd,0xd3,0x00};

int main( )

...
```

尽管我们成功使用了 Bash 单行命令，但我们的代码并不干净，也不太容易重用。让我们把所有内容整合到一个 Bash 脚本来解决这些问题：

```bash
kali@kali:~$ cat dlspoils.sh

#!/bin/bash

# Bash 脚本，用于搜索给定的利用工具并下载所有匹配项。

for e in $(searchsploit afd windows -w -t | grep http | cut -f 2 -d "|")
do
  exp_name=$(echo $e | cut -d "/" -f 5)
  url=$(echo $e | sed 's/exploits/raw//')
  wget -q --no-check-certificate $url -O $exp_name
done
```

```
kali@kali:~$ chmod +x ./dlspoils.sh
kali@kali:~$ ./dlspoils.sh
```
