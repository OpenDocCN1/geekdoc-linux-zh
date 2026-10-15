
D: file: `/usr/src/majordomo-1.94.4/man/total.local`: create

D: file: `/usr/lib/majordomo/Tools/action`: create

D: file: `/usr/lib/majordomo/Tools/archive.pl`: create

D: file: `/usr/lib/majordomo/Tools/archive_mh.pl`: create

D: file: `/usr/lib/majordomo/Tools/digest.send`: create

D: file: `/usr/lib/majordomo/Tools/logsummary.pl`: create

D: file: `/usr/lib/majordomo/Tools/makeindex.pl`: create

D: file: `/usr/lib/majordomo/Tools/new-list`: create

D: file: `/usr/lib/majordomo/Tools/sequencer`: create

D: file: `/usr/lib/majordomo/Tools/archive2.pl`: create

D: file: `/usr/lib/majordomo/bin/action`: create

D: file: `/usr/lib/majordomo/bin/approve`: create

D: file: `/usr/lib/majordomo/bin/bounce`: create

D: file: `/usr/lib/majordomo/bin/medit`: create

D: file: `/usr/lib/majordomo/bin/bounce-remind`: create

D: file: `/usr/lib/majordomo/config-test`: create

D: file: `/usr/lib/majordomo/config_parse.pl`: create

D: file: `/usr/lib/majordomo/contrib/MajordomoCreate`: create

D: file: `/usr/lib/majordomo/contrib`: create

D: file: `/usr/lib/majordomo/digest`: create

D: file: `/usr/lib/majordomo/majordomo`: create

D: file: `/usr/lib/majordomo/majordomo_pl`: create

D: file: `/usr/lib/majordomo/majordomo_version.pl`: create

D: file: `/usr/lib/majordomo/request-answer`: create

D: file: `/usr/lib/majordomo/resend_action`: create

D: file: `/usr/lib/majordomo/sample_cf`: create

D: file: `/usr/lib/majordomo/shlock`: create

D: file: `/usr/lib/majordomo/wrapper`: create

D: file: `/usr/man/man1/approve.1`: create

D: file: `/usr/man/man1/bounce-remind.1`: create

D: file: `/usr/man/man1/bounce.1`: create

D: file: `/usr/man/man1/bulk_mailer.1`: create

D: file: `/usr/man/man1/digest.1`: create

```
```

D: file:`/usr/man/man1/resend`: create

D: file:`/usr/man/man8/majordomo.8`: create

D: file:`/usr/sbin/bulk_mailer`: create

D: file:`/var/lib/majordomo`: create

D: file:`/var/lib/majordomo/OLDLOGS`: create

D: file:`/var/lib/majordomo/archives`: create

D: file:`/var/lib/majordomo/digest`: create

D: file:`/var/lib/majordomo/lists`: create

D: file:`/var/lib/majordomo/tmp`: create

```
(运行安装前和安装后脚本，这些脚本会创建 majordomo 用户和组)

# 配置 majordomo

应该在 `/etc/aliases` 文件中添加多个别名。这些别名允许相关账户以不同的名称列出。

## Majordomo 别名
- listserve listserv
listserver: listserv
majordomo: listserv
listserv: "| /usr/lib/majordomo/wrapper majordomo"
majordomo-owner: owner-majordomo
owner-majordomo: owner-listserv
listserv-owner: owner-listserv
owner-listservser: mailserververguy@mybox.com

## 列表别名
### 生化学列表
- biochem-request: "| /usr/lib/majordomo/wrapper request-answer biochemistry
biochem-approval: biochemistry
biochem-owner: owner-biochem
owner-biochem: email@mybox.com
biochem: "| /usr/lib/majordomo/wrapper resend -1 biochemistry -h mail.mybox.com -R Biochem-out"
biochem-out: include:/var/lib/majordomo/lists/biochem,biochem-archival
biochem-archival: "| /usr/lib/majordomo/wrapper archive2.pl -a -M -f /var/lib/majordomo/archives/biochem/biochem

接下来的区块建立了一个与生物化学相关的列表。与列表服务器本身，每个列表都有一个所有者，所有者可以控制配置并接收错误消息。发送到地址 `biochem@mail.mybox.com` 的每条消息都会分发给 `/var/lib/majordomo/lists/biochem` 文件列出的接收者。消息也会发送给 `archive2.pl` Perl 脚本。存档的消息存储在如 `/var/lib/majordomo/archives/biochem/biochem.199907` 等文件中（这是 1999 年 7 月的存档）。

## 运行 majordomo

遗憾的是，这些精彩的功能目前还没有完全可用。首先，需要重新构建别名数据库，应使用 `newalases` 命令或 `sendmail -bi`。接下来，由于所有直接传递给程序的邮件都由 `smrsh` 程序处理，因此它需要被配置为允许 majordomo 的封装程序接收邮件。要实现这一点，只需使用以下命令创建适当的符号链接：

```
ln -s /var/lib/majordomo/wrapper /etc/smrsh/wrapper
```

建议将行 `Tmajordomo` 添加到 `/etc/sendmail.cf` 文件中，以避免任何额外的 X-Authentication-Warning 头部行。

现在可以测试列表服务器了。运行以下命令：

```
echo "help" | majordomo@mail.mybox.com
```
