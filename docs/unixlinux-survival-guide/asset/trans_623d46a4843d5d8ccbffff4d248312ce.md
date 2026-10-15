

</item>
</channel>
</rss>

Listing 6.24 中显示的文件使用了规范中的另一个特性。`<link>` 标签中的 URL 指向包含有关新闻项目详细信息的 Web 地址。大多数新闻阅读器会在用户双击该项目时打开此 URL。文件的结构并不复杂，但手工维护它容易出错，并给新闻维护者带来不必要的负担。为了在某种程度上自动化该过程，你可以使用 Listing 6.25 中显示的脚本。

## LISTING 6.25 Script for Generating the RSS File

```
#!/usr/bin/sh
# $Id: genrss1.sh,v 1.2 2004/09/13 11:31:46 erikk Exp erikk $
########################################################
#
#    file:         genrss1.sh
#    purpose:      generates an rss 2.0 feed from
#                  the files stored in the directory
#                  articles
#    author:       Erik Keller
#    parameters:   none
########################################################

# Variables
WORKDIR=/export/home/users/erikk/work/newstick
ARTICLEDIR=$WORKDIR/articles
RSSFILENAME=$WORKDIR/internalnews.rss

# create the header
echo "<rss version=\"2.0\">" > $RSSFILENAME
echo "<channel>" >> $RSSFILENAME
echo "<title>example.domain internal news</title>" >> $RSSFILENAME
echo "<link>http://internalweb.example.domain</link>" >> $RSSFILENAME
echo "<description>example.domain internal newswire</description>" >> $RSSFILENAME
echo "<language>en</language>" >> $RSSFILENAME
```

```
# get the articles
THENews=`ls -t $ARTICLEDIR`

for i in $THENews
 do
    cat $ARTICLEDIR/$i >> $RSSFILENAME
done

# create the footer
echo "</channel>" >> $RSSFILENAME
echo "</rss>" >> $RSSFILENAME
# EOF
```

该脚本并不是一个功能齐全的 RSS 编辑器，它只是自动化了以下步骤：它创建 RSS 文件的头部部分，并获取 articles 目录中找到的文件列表，按时间戳排序 `ls -t`。找到的文件内容会被追加到 RSS 文件中，最新的在前；在追加完最后一个项目后，会添加 channel 和 rss 的闭合标签。articles 目录中的新闻项目内容如 Listing 6.26 所示。

## LISTING 6.26 News Item in Directory articles

```
<item>
<title>The Cluster will be upgraded to 1024 CPUs</title>
<link>http://internalweb.example.domain/cpucluster.html</link>
<description>
The SUN cluster will be expanded to 1024 CPUs starting next week.
There are no downtimes expected during the upgrade phase, all
GRID apps should continue running as expected. The increased speed
should help us to achive the set goals regarding the calculations.
Thank you
</description>
</item>
```

像所示这样一个文件要容易得多创建和维护，并且使用上述脚本可以确保最新添加的内容会首先显示在 feed 中。RSS 文件通过 Web 服务器使用 HTTP 协议分发或作为文件分发。由于 feed 的维护者可以决定创建多少个不同的文件，从而创建多少个 feed，使用这种机制不仅可以让你以一种不会淹没在每日邮件风暴中的方式让用户了解他们所连接网络的新发展，而且还可以成为你同事系统管理员的共同参考点。如果你让监控脚本也以这种格式写入其消息，所有相关人员都能够使用单一的信息点来保持最新。你只需要确保区分谁可以访问什么信息；例如，关于监控脚本的一些数据绝对不适合公开发布。

完整的规范可在 http://blogs.law.harvard.edu/tech/rss 找到。

## 6.2.2.5 The script Command

如果需要将所有命令及其响应记录到文件中以用于文档目的或其他用途，`script` 命令就可以提供帮助。它将终端窗口中出现的所有内容复制到一个文件中。这种方法在你想要运行测试、想要尝试了解一个新程序（当然是在终端中运行），或只是想记录你所做的事情时特别方便。Listing 6.27 演示了该程序的使用。

## LISTING 6.27 Recording a Terminal Session Using Script

```
root@unixhost> script logadmex1.txt
Script started, file is logadmex1.txt
root@unixhost> crontab -l | grep logadm
10 3 * * * /usr/sbin/logadm
root@unixhost> /usr/sbin/logadm
root@unixhost> ls -l /var/adm/message*
-rw-r--r-- 1 root root 63521 Sep 26 14:58 /var/adm/messages
-rw-r--r-- 1 root root 338591 Sep 21 15:43 /var/adm/messages.0
-rw-r--r-- 1 root root 352923 Sep 8 03:10 /var/adm/messages.1
-rw-r--r-- 1 root root 84875 Aug 28 03:10 /var/adm/messages.2
-rw-r--r-- 1 root root 399605 Aug 18 14:33 /var/adm/messages.3
root@unixhost> Script done, file is logadmex1.txt
root@unixhost> cat logadmex1.txt
Script started on Sun Sep 26 14:58:26 2004
root@unixhost> crontab -l | grep logadm
10 3 * * * /usr/sbin/logadm
root@unixhost> /usr/sbin/logadm
root@unixhost> ls -l /var/adm/message*
-rw-r--r-- 1 root root 63521 Sep 26 14:58 /var/adm/messages
-rw-r--r-- 1 root root 338591 Sep 21 15:43 /var/adm/messages.0
-rw-r--r-- 1 root root 352923 Sep 8 03:10 /var/adm/messages.1
-rw-r--r-- 1 root root 84875 Aug 28 03:10 /var/adm/messages.2
-rw-r--r-- 1 root root 399605 Aug 18 14:33 /var/adm/messages.3
root@unixhost>
script done on Sun Sep 26 14:58:53 2004
```

