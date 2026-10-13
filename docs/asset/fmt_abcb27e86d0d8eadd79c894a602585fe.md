
`MASTERDIR=//Master` `TOOLDIR=./Tools`

`./Tools/Configure` `sendmail.def` > `sendmail.cf`

`m -f sendmail.cf tmp sendmail.cf`

`[root@server CF-3.7tpl2#]`

> 请确保输入正确的文件名（`sendmail.cf`，而不是 `sendmail.def`）。

![](img/d549b948a29b14d0d8313a8ed09b5698_181_0.png)

## 6 停止 sendmail。

停止一次 sendmail 以验证配置文件是否已正确写入。

输入命令。

```bash
[root@server CF-3.7tpl2#] make sendmail.cf

MASTERDIR=//Master TOOLDIR=./Tools

./Tools/Configure sendmail.def > sendmail.cf

m -f sendmail.cf tmp sendmail.cf

[root@server CF-3.7tpl2#] /etc/rc.d/init/sendmail stop

Shutting down sendmail: sendmail

[root@server CF-3.7tpl2#]
```

## 7 在测试模式下启动 sendmail。

切换到测试模式以验证 Linux 中是否可以发送邮件。

输入命令。

```bash
[root@server CF-3.7tpl2#] /etc/rc.d/init/sendmail stop

Shutting down sendmail: sendmail

[root@server CF-3.7tpl2#] /usr/sbin/sendmail -bt -C.sendmail.cf

ADDRESS TEST MODE (RULESET 3 NOT automatically invoked)

Enter <ruleset><address>
```

## 8 执行测试发邮件。

输入 "@" 和邮箱地址（在 Linux 中注册的用户名以及 `sendmail.def` 中的域名）。

| > Bob@Coriolis.com |
| rewrite: ruleset 0 input: Bob@coriolis.com |
| rewrite: ruleset 97 input: Bob@coriolis.com |
| rewrite: ruleset 3 input: Bob@coriolis.com |
| rewrite: ruleset 86 input: Bob@coriolis.com > |
| rewrite: ruleset 96 input: Bob@coriolis.com > |
| rewrite: ruleset 3 returns: Bob@coriolis.com > |
| rewrite: ruleset 0 returns: Bob@coriolis.com > |
| rewrite: ruleset 97 input: Bob |
| rewrite: ruleset 3 input: Bob |
| rewrite: ruleset 0 input: Bob |
| rewrite: ruleset 0 returns: $$ local: Bob |
| rewrite: ruleset 97 returns: $$ local: Bob |
| rewrite: ruleset 0 returns: $$ local: Bob |
| rewrite: ruleset 97 returns: $$ local: Bob |

![](img/d549b948a29b14d0d8313a8ed09b5698_181_1.png)

172 * With Aster*

## 10.3 创建邮件服务器部分 1

退出测试模式。

```bash
在显示提示符时按下 Ctrl+D。

rewrite: ruleset 97 returns: $* local$: Bob

rewrite: ruleset 0 returns: $* local$: Bob

>Ctrl--D

>0 Bob

rewrite: ruleset 0 input: Bob

rewrite: ruleset 0 returns: $* local$: Bob

>root@server CF-3.7Wp12#*

显示了正常的提示符。
```

## 10 保存原始配置文件。

更改当前配置命名并保存。输入命令。

```bash
>root@server CF-3.7Wp12#* mv /etc/sendmail.cf /etc/sendmail.cf.orig

>root@server CF-3.7Wp12#* _
```

## 11 复制配置 sendmail.cf。

复制创建的 `sendmail.cf`。输入命令。

```bash
>root@server CF-3.7Wp12#* mv /etc/sendmail.cf /etc/sendmail.cf.orig

>root@server CF-3.7Wp12#* cp sendmail.cf /etc

>root@server CF-3.7Wp12#* _
```

## 12 启动 sendmail。

切换目录。

```bash
>root@server CF-3.7Wp12#* cp sendmail.cf /etc

>root@server CF-3.7Wp12#* cd /etc/rc.d/init.d

>root@server init.d#* ../init.d start

Starting sendmail: sendmail

>root@server init.d#*
```
