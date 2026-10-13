
# 服务器 RBL 检查

`num_check_received` 3

## 修改 RBL 默认评分

默认情况下，`bl.spamcop.net` RBL 分数为 0（禁用）。

我们将覆盖此设置并给任何命中 3 分

有关此 RBL 的信息可以从 `http://spamcop.net/for-service/cache/290.html` 获取

`score RCVD_IN_BL_SPAMCOP_NET 3`

## 从源码安装设置 spamd 和 spamp

如果你没有执行 CPAN 安装，下一步是将 `spamd`（守护进程）和 `spamp`（客户端）二进制文件复制到适当目录，并创建所需的 SpamAssassin 在系统启动时运行的启动脚本：

```
cd /usr/local/src/mailserver/Mail-SpamAssassin*
cd spamd
cp spamp /usr/bin
cp spam /usr/bin
cp redhat-rc-script.sh /etc/init.d/spamd
service spamd start
```

## 通过 CPAN 安装设置 spamd 和 spamp

如果你之前使用 CPAN 安装了 SpamAssassin，你需要复制以下文件来启动 `spamd` 守护进程。运行以下命令：

```
cp /root/.cpan/build/Mail-SpamAssassin-2.63/redhat-rc-script.sh /etc/init.d/spamd
cd /root/.cpan/build/Mail-SpamAssassin-2.63/spamd
cp spamd /usr/bin
cp spamd /usr/bin
service spamd start
```

## 运行 spamd

现在，SpamAssassin 应该正在运行。让我们看看：

```
ps aux | grep spamd
```

输出应该类似于下面：

```
root 13368 10.1 2.1 25780 21172 ? S 17:09
↳ 0:00 /usr/bin/spamd -d -c -a -m5 -H
```

root 13383 0.0 0.0 4144 584 pts/2 S 17:09

↳ 0:00 grep spam

```

恭喜——你已经设置好了 SpamAssassin。让我们进入下一步，Qmail-Scanner。

## 安装 Qmail-Scanner

按照以下步骤安装 Qmail-Scanner：

1. Qmail-Scanner 需要安装 `tnef`，所以请先处理好它：

```
cd /usr/local/src/mailserver/tnef*
./configure
make
make install
```

2. 安装 Qmail-Scanner 使用的 `mailrop`：

```
cd /usr/local/src/mailserver/mailrop*
./configure
make
make install
```

在开始安装 Qmail-Scanner 之前，你需要确保已安装了 `perl-suidperl`。你可以通过使用 `rpm -q perl-suidperl` 查询 RPM 数据库来查找此内容的 RPM 版本，如果包已安装即可继续。如果没有，请检查 `rpm.pbone.net` 获取 Fedora Core 2 的包。

3. 安装 Qmail-Scanner：

```
cd /usr/local/src/mailserver/qmail-scanner*
groupadd qscand
adduser -c 'qmail-Scanner Account' -g qscand -s /bin/false qscand
./configure --scanners
--clamscan -c verbose_spammassassin --admin *"
--domain 'yourdomain.com' --install
```

4. 按照屏幕提示操作。

5. 完成后，运行以下命令：
`setuidgid qmail /var/qmail/bin/qmail-scanner-queue.pl -g`

如果你看到如下输出：

```
perlscanner: generate new DB file from
/var/spool/qmailscanner/quarantine-attachments.txt
perlscanner: total of 9 entries.
```

那么你就已经设置好了 Qmail-Scanner。

## 配置 Qmail-Scanner

Qmail-Scanner 是一个位于 `/var/qmail/bin` 的 Perl 脚本，名为 `qmail-scanner-queue.pl`。如果你用文本编辑器编辑它，你会看到可以为服务器配置的大量选项。大多数配置选项都有良好的文档，因此我们在这里不再介绍。

以下是配置 Qmail-Scanner 的步骤：

1. 你的首要任务是修改 `qmail-scanner-queue.pl`。用文本编辑器打开它并找到选项数组。你可以根据需要更改选项。例如，如果你想更改隔离评分，找到 `quarantine_score` 所在并更改值。

2. 一旦你做了更改，重启 `qmail-scanner-queue.pl`。你可以通过运行以下命令来实现：

```
/var/qmail/bin/qmail-scanner-queue.pl -restart
```
