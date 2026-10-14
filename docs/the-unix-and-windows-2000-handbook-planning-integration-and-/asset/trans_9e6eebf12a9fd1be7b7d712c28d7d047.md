

```
# Copyright (c) 1998 Sendmail, Inc. All rights reserved.
# Copyright (c) 1983 Eric P. Allman. All rights reserved.
# Copyright (c) 1988, 1993
#
# The Regents of the University of California. All rights reserved.
#
#
# By using this file, you agree to the terms and conditions set
# forth in the LICENSE file which can be found at the top level of
# the sendmail distribution.
#
#
#
# The following is a generic domain file. You should be able to
# use it anywhere. If you want to customize it, copy it to a file
# named with your domain and make the edits; then, copy the appropriate
# .mc files and change `DOMAIN(generic)' to reference your updated domain
# files.
#
divert(0)
VERSIONID(`@(#)generic.m4	8.9 (Berkeley) 5/19/1998')
define(`confFORWARD_PATH',
`$:/.forward.$w:$:/.forward.$h:$:/.forward.$w:$:/.forward')dnl
FEATURE(redirect)dnl
FEATURE(use_cw_file)dnl
```

sendmail.cf 的主配置文件位于 cf 目录（cf/cf）中。该目录包含根据你所使用的 UNIX 版本类型命名的通用文本配置文件（例如 generic-hpux10.mc、generic-solaris2.mc 等）。请尝试选择一个与你的工作站/服务器最匹配的通用文件。复制该文件，并赋予它你的域名。

我们将配置一台 Linux 工作站作为 sniglets.com 的主邮件服务器。选择 tcpproto.mc 文件作为开发我们的配置文件的模板。复制 tcpproto.mc 文件，但将名称改为你的域名（sniglets.com.mc，清单 9.2）。

主配置文件 sniglets.com.mc 必须包含一个 OSTYPE 行。文件和队列的位置由该宏控制。ostype 目录中包含每个受支持操作系统对应的文件。找到你的操作系统，并将 unknown 改为适用的操作系统（linux）。

OSTYPE 行应位于 VERSIONID 行之后的第一行。

之前，我们在 domain 目录中创建了一个 sniglets.com.m4 文件。为了包含该文件中定义的宏和功能，我们需要在配置文件中添加一个 DOMAIN 行。该行应放在 OSTYPE 行之后。在 sniglets.com.mc 中输入以下行：

```
DOMAIN(sniglets.com)
```

最后两行指定邮件程序（mailer）类型。MAILER(local) 行配置 local 和 prog MDA。local MDA 将邮件投递给本地机器上的用户。prog MDA 允许通过程序“管道”投递邮件。如果所有邮件只是被中继转发，则不需要此项。

### 清单 9.2 sniglets.com 的主配置文件

```
divert(-1)
#
# Copyright (c) 1998 Sendmail, Inc.  All rights reserved.
# Copyright (c) 1983 Eric P. Allman.  All rights reserved.
# Copyright (c) 1988, 1993
#     The Regents of the University of California.  All rights reserved.
#
# By using this file, you agree to the terms and conditions set
# forth in the LICENSE file which can be found at the top level of
# the sendmail distribution.
#
#
# This is the prototype file for a configuration that supports nothing
# but basic SMTP connections via TCP.
#
# You MUST change the 'OSTYPE' macro to specify the operating system
# on which this will run; this will set the location of various
# support files for your operating system environment.  You MAY
# create a domain file in ../domain and reference it by adding a
# 'DOMAIN' macro after the 'OSTYPE' macro.  I recommend that you
# first copy this to another file name so that new sendmail releases
# will not trash your changes.
#
divert(0)dnl
VERSIONID(`@(#)tcpproto.mc        8.10 (Berkeley) 5/19/1998')
OSTYPE(unknown)
MAILER(local)
MAILER(smtp)
```

最后一行 MAILER(smtp) 启用简单邮件传输协议（SMTP）。该行激活 SMTP、扩展 SMTP、SMTP8（不将 8 位数据转换为 MIME 的 SMTP）以及中继功能。该行使我们的 Linux 邮件服务器能够与互联网上的其他部分交换邮件。该行假设所有邮件程序都在运行 DNS。

