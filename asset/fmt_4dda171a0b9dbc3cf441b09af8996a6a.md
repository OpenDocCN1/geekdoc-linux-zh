
# output the matches in a friendly and useful format.

```bash
screen="egrep -vE '(/usr/bin|/bin)'"

echo "Executable SUID programs found on the system:"

for match in `find / -type f -perm +4000 -print | $screen`
do

  if [ -x $match ] ; then

    owner=`ls -l $match | awk '{print $3}'`

    lastmod=`ls -ld $match | awk '{print $6" "$7" "$8}'`

    echo " $match (owner is '$owner' and lastmod is $lastmod)"

  fi

done

exit 0
```

当以root身份运行（当然，这样你才能看到系统上的每个文件）时，输出如下所示：

```text
# findsuid

Executable SUID programs found on the system:

/usr/bin/suidperl (owner is "root" and lastmod is Aug 9 2001)

/usr/bin/sperl5.8.0 (owner is "root" and lastmod is Aug 9 2001)

/usr/bin/chage (owner is "root" and lastmod is Aug 27 2001)

/usr/bin/passwd (owner is "root" and lastmod is Aug 27 2001)

/usr/bin/at (owner is "root" and lastmod is Aug 2 2001)

/usr/bin/chfn (owner is "root" and lastmod is Aug 6 2001)

/usr/bin/chsh (owner is "root" and lastmod is Aug 26 2001)

/usr/bin/newgrp (owner is "root" and lastmod is Aug 26 2001)

/usr/bin/crontab (owner is "root" and lastmod is Jun 24 2001)

/usr/bin/kcheckpass (owner is "root" and lastmod is Sep 8 2001)

/usr/bin/ssh (owner is "root" and lastmod is Sep 6 2001)

/usr/bin/rcp (owner is "root" and lastmod is Jul 24 2001)

/usr/bin/login (owner is "root" and lastmod is Jul 24 2001)

/usr/bin/rsh (owner is "root" and lastmod is Jul 24 2001)

/usr/bin/sudo (owner is "root" and lastmod is Jul 23 2001)

/usr/sbin/ping6 (owner is "root" and lastmod is Aug 27 2001)

/usr/sbin/traceroute6 (owner is "root" and lastmod is Aug 27 2001)

/usr/sbin/sendmail (owner is "root" and lastmod is Aug 31 2001)

/usr/sbin/usernetctl (owner is "root" and lastmod is Sep 9 2001)

/usr/sbin/userhelper (owner is "root" and lastmod is Aug 27 2001)

/usr/sbin/traceroute (owner is "root" and lastmod is Jun 25 2001)

/usr/sbin/suexec.old (owner is "root" and lastmod is Sep 5 2001)

/usr/X11R6/bin/Xwrapper (owner is "root" and lastmod is Sep 5 2001)

/bin/ping (owner is "root" and lastmod is Aug 27 2001)

/bin/mount (owner is "root" and lastmod is Jul 24 2001)

/bin/umount (owner is "root" and lastmod is Jul 24 2001)

/bin/su (owner is "root" and lastmod is Jul 23 2001)

/sbin/pwdck_chkpwd (owner is "root" and lastmod is Sep 24 2001)

/sbin/unix_chkpwd (owner is "root" and lastmod is Sep 24 2001)
```

输出非常有趣，如果你使用有用的`diff`命令并归档早期输出以便自动比较，你将拥有一个非常有用的工具，可以帮助快速识别可能存在的特洛伊木马。

## 4. 你的系统上有数百个不同的shell脚本，你可以用一个脚本来找到它们：

```bash
# cat findscripts
#!/bin/sh

for match in `find / -type f -perm +0111 -print`
do

  if [ "`file $match | grep -i 'shell script:'`" != "" ]; then

    echo $match is a shell script

  fi

done
```
