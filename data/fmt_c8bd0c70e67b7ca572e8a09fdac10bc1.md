
如果一切正常，准备好安装插件。

## Vpopmail

现在我们将在服务器上安装 `vpopmail`：

- 1. 首先为 `vpopmail` 添加我们的账户和组：
```bash
cd /usr/local/src/mailserver/vpopmail

groupadd -g 109 vchpw

useradd -g vchpw -u 109 -d /home/vpopmail vpopmail

./configure --enable-roaming-users=y

make

make install

crontab -e
```

- 2. 将以下内容添加到 `crontab`：
```
40 * * * /home/vpopmail/bin/clearopensmtp 2>&1 > /dev/null
```

- 3. 创建管理员账户并确保为用户和域名替换正确信息：
```bash
cd /home/vpopmail/bin

./vaddomain yourdomain.com

./vadder admin@yourdomain.com
```

## Courier-IMAP

接下来我们将安装 `Courier-IMAP`：

- 1. 首先，编译并安装二进制文件：
```bash
cd /usr/local/src/mailserver/

chown -R someuser:someuser courier-imap*

su someuser

cd /usr/local/src/mailserver/courier-imap*

./configure --with-redhat

exit

cd /usr/local/src/mailserver/courier-imap*

make

make install

make install-configure
```

- 2. 再次忽略收到的任何错误。然后将 IMAP 作为服务添加：
```bash
cp courier-imap.sysinit /etc/init.d/imapd
```
> 当 `make` 命令尝试编译 `authchkpw` 时可能会遇到错误。忽略此错误并继续。

- 3. 添加并启动服务：
```bash
chkconfig --add imapd

/etc/init.d/imapd
```

## POP3

我们将为服务器安装 POP3 支持：

- 1. 首先，创建目录并开始运行文件：
```bash
mkdir -p /var/qmail/supervise/qmail-pop3d

mkdir -p /var/qmail/supervise/qmail-pop3d/log/

mkdir -p /var/log/pop3d

pico /var/qmail/supervise/qmail-pop3d/run
```

- 2. 添加以下内容：
```bash
#!/bin/sh

exec /usr/local/bin/softlimit -m 2000000 \

/usr/local/bin/tcpserver -v R -H 0 110 \

/var/qmail/bin/qmail-popup \

yourdomain.com /home/popmail/bin/vchkpw \

/var/qmail/qmail-pop3d Mailird 2>&1
```
在上面的示例中将 `yourdomain.com` 替换为你的域名。

- 3. 现在编辑运行文件：
```bash
pico /var/qmail/supervise/qmail-pop3d/log/run
```

- 4. 添加以下内容：
```bash
#!/bin/sh

exec /usr/local/bin/setuidgid qmail \

/usr/local/bin/multilog t \

/var/log/qmail/pop3d
```

- 5. 设置权限并链接文件：
```bash
chown qmail /var/log/qmail/pop3d

chmod 755 /var/qmail/supervise/qmail-pop3d/run

chmod 755 /var/qmail/supervise/qmail-pop3d/log/run

ln -s /var/qmail/supervise/qmail-pop3d /service
```

- 6. 你快完成了！现在你需要编辑 `/var/qmail/bin/qmailctl` 脚本并添加 `qmail-pop3d` 的信息：
```bash
pico /var/qmail/bin/qmailctl
```

在启动（start）部分，在两个分号上方直接添加以下内容：
```
if svok /service/qmail-pop3d ; then

svc -u /service/qmail-pop3d /service/qmail-pop3d/log

else

echo qmail-pop3d supervise not running

fi
```

在停止（stop）部分，在两个分号上方直接添加以下内容：
```
echo qmail-pop3d*

svc -d /service/qmail-pop3d /service/qmail-pop3d/log
```

在状态（stat）部分，在 `qmail-qstat` 部分上方直接添加以下内容：
```
svstat /service/qmail-pop3d

svstat /service/qmail-pop3d/log
```

在暂停（pause）部分，在两个分号上方直接添加以下内容：
```
echo Pausing qmail-pop3d

svc -p /service/qmail-pop3d
```

在继续（cont）部分，在两个分号上方直接添加以下内容：
```
echo Continuing qmail-pop3d

svc -c /service/qmail-pop3d
```

在重启（restart）部分，在两个分号上方直接添加以下内容：
```
echo * Restarting qmail-pop3d.*

svc -t /service/qmail-pop3d /service/qmail-pop3d/log
```

- 7. 保存此文件，然后重启 `qmail`：
```
qmailctl stop

qmailctl start
```

# Clam 反病毒 (Clam AntiVirus)

现在我们准备好安装 Clam 反病毒软件了：

- 1. 首先创建相应的组和用户，编译并安装二进制文件，然后再次编辑 `crontab`：
```
cd /usr/local/src/mailserver/clamav*

groupadd clamav

useradd -g clamav -s /bin/false -c "Clam AntiVirus" clam

./configure

make

make install

touch /var/log/clam-update.log
```
`chmod 600 /var/log/clam-update.log`
`chown clamav /var/log/clam-update.log`
`freshclam -d -c 2 -1 /var/log/clam-update.log`
`crontab -e`

- 2. 添加以下内容：
```
0 8 * * * /usr/local/bin/freshclam -quiet -1 /var/log/clam-update.log
```

- 3. 现在链接文件：
```
/usr/local/bin/freshclam -1 /var/log/clam-update.log
```

# qmail-Scanner

是时候安装 `qmail-Scanner` 了：

- 1. 制作并安装适当的文件：
```
cd /usr/local/src/mailserver/tnef*

./configure

make

make install
```

```
cd /usr/local/src/mailserver/maildrop

./configure

make

make install
```

> 在开始之前，你需要确保已安装 `perl-superlog`。你可以先通过 `rpm -q perl-superlog` 查询 RPM 数据库来查找此 RPM 版本。如果已安装该包，可以继续。如果没有，请检查 `rpm.bone.net` 获取 Fedora Core 2 的包。

> 如果你安装的 `perl-superlog` 版本需要更新 Perl，请确保在继续后续操作之前，所有其他模块均工作正常。在某些情况下，你可能需要重新安装模块。

- 2. 继续执行以下操作：
```
cd /usr/local/src/mailserver/qmail-scanner*

groupadd qscand
```
