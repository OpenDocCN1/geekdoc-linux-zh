
`R` 表示该行是一条规则，`lhs` 是规则的左侧，`rhs` 是规则的右侧，`description` 是供人类解释该规则作用的注释。左侧是匹配特定邮件头部的规范，而右侧指定了找到匹配项后要执行的操作。

正如使用 `lex`、`yacc` 和 `JavaCC` 可以根据匹配的令牌（`tokens`）指定操作一样，`sendmail` 解析器也是这样运行的。`sendmail.cf` 文件由 `sendmail` 解析，它识别左侧的若干几个指定符：

- `$- $` 匹配单个令牌。
- `$*\ $` 匹配任意数量的令牌，包括零个令牌。
- `$\$*+` 匹配任何大于零数量的令牌。
- `$=character$` 匹配任何等于该字符的令牌。

如果规则陈述的这些指定符找到了匹配项，则可能由一个或多个右侧指定符执行一个或多个操作：

- `$- $@$` 重写并返回。
- `$*\integer$` 使用整数指定的规则集进行重写。
- `$\%` 投递到指定的投递器（`mailier`）。
- `$\$character \$integer$` 在左侧定义的变量上执行操作。

例如，考虑一条向邮件服务器添加 FQDN（完全限定域名）的规则，其中消息的目标是外部投递。在这种情况下，`$h`（主机）被设置为 `mail`，`$d`（域名）被设置为 `companyA.com`。因此，匹配没有 FQDN 的用户名的规则为：

```
R$+ $$@1<$h$.d> 为用户名添加 FQDN
```

因此

`paul@mail.companyA.com`

对于一个具有多个内部网络的更复杂的组织，更复杂的规则可能在 FQDN 的公司名称上方有第二层级（例如，`companyA.com` 销售部门的邮件服务器其 FDN 为 `mail.sales.companyA.com`）。在这种情况下，你定义 `$o`（组织层级），将 `$o` 设置为 `sales`，并将规则更改为：

```
R+$      $@1c=$sh.$o.$d      为用户名添加 FQDN，包括组织层级
```

因此，任何有效的 Solaris 用户名（如 `nei`）都会在其后附加 `mail`、一个点 `()`、`sales`、另一个点以及 `companyA.com` 用于外部传输：

```
weil@mail.sales.companyA.com
```

因此，规则、宏和选项的组合可以成功创建并解析大多数电子邮件地址。如果对于第一次担任 `sendmail` 管理员来说，所有的规则编写和选项设置似乎很困难，可以使用基于 GUI 的配置工具减轻负担。运行和配置 `sendmail` 最简单的方法之一是使用 `webmin`，它可以在 `http://www.webmin.com/` 免费获取。`webmin` 是一个用于 Solaris 系统管理（包括 `sendmail`）的 Web 界面。使用任何支持表格和表单的浏览器可以使用 `sendmail` 配置模块，允许管理员管理 `sendmail` 别名、伪装、地址重写和其他功能。`webmin` 还可以使用 SSL 保护 Web 浏览器与服务器之间的连接，这对于远程管理特别有用。图 27-3 显示了 `webmin` 界面及其支持的配置 `sendmail` 选项。

![](img/11bcccd1804574cca0c3018732958dd5_586_0.png)

图 27-3 配置 `sendmail` 的 `webmin` GUI

# 第 27 章：Sendmail

## 运行 sendmail

`sendmail` 作为守护进程启动，通过通常在多用户启动期间（`/etc/rc2`）激活的脚本运行。要手动停止 `sendmail`，使用以下命令：

```
/etc/init.d/sendmail stop
```

启动 `sendmail`，使用此命令：

```
/etc/init.d/sendmail start
```

## 故障排除

由于 `sendmail` 可能是一个配置的程序，`sendmail` 还包含了一些故障排除措施。例如，命令

```
server# sendmail -bt
```

会导致 `sendmail` 在地址测试模式下运行，这在将规则集引入生产系统之前进行测试非常有用。请记住，规则集 3 不会在地址测试模式下自动调用：因此，测试地址 `Paul.Watters.1996@pem.cam.ac.uk` 应该使用测试字符串

```
"3,0 Paul.Watters.1996@pem.cam.ac.uk"
```

而不是仅使用

```
"0 Paul.Watters.1996@pem.cam.ac.uk!"
```

作为一个完整的示例：

```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)

nter <ruleset><address>

> 0 Paul.Watters.1996@pem.cam.ac.uk  Watters  1996 @ pem  cam  ac  uk

rewrite: ruleset 0  input: Paul  Watters  1996 @ pem  cam  ac  uk

rewrite: ruleset 19 input: Paul  Watters  1996 @ pem  cam  ac  uk

rewrite: ruleset 19 returns: Paul  Watters  1996 @ pem  cam  ac  uk

rewrite: ruleset 98  input: Paul  Watters  1996 @ pem  cam  ac  uk

rewrite: ruleset 98 returns: Paul  Watters  1996 @ pem  cam  ac  uk

rewrite: ruleset 98  input: Paul  Watters  1996 @ pem  cam  ac  uk

rewrite: ruleset 98 returns: # local : Paul  Watters  1996 @ pem  cam

ac  uk

rewrite: ruleset 0 returns: $ local : Paul  Watters  1996 @ pem  cam

ac  uk

Watters.1996@pem.ac.uk

> 0 Paul.Watters.1996@pem.cam.ac.uk

rewrite: ruleset 0  input: Paul  Watters  1996 @ pem  cam  ac  uk

rewrite: ruleset 199 input: Paul  Watters  1996 @ pem  cam  ac  uk

rewrite: ruleset 199 returns: Paul  Watters  1996 @ pem  cam

ac  uk

rewrite: ruleset 98  input: Paul  Watters  1996 @ pem  cam  ac  uk

rewrite: ruleset 98 returns: $ local : Paul  Watters  1996 @ pem  cam

ac  uk

rewrite: ruleset 0 returns: $ local : Paul  Watters  1996 @ pem  cam

ac  uk

rewrite: ruleset 3 input: $ local : Paul  Watters  1996 @ pem  cam

ac  uk

rewrite: ruleset 3 returns: $ local : Paul  Watters  1996 @ pem  cam

ac  uk
```

除了基于信息的故障排除外，`mailx` 还有一个 `-v`（详细）开关，可以跟踪邮件发送后的投递过程。例如，如果邮件从 `client.companyA.com` 发送到 `user@companyB.com`，投递过程如下：

```
client mailx -v user@companyB.com

Subject: Hello

Hi user@companyB.com. This is a test.

DOT

client@companyB.com... Connecting to mailhost (mail)...

220 mail.server.com ESMTP Mail 8.12.10; Sat, 19 Feb 2002 12:23:12 +0000

(EST)

>>> HELLO mail@companyA.com

220 mail.server.com Hello mail@companyA.com (moppet.companyA.com), pleased to meet you

>>> MAIL FROM:<user@companyA.com>

250 user@companyA.com... Sender ok

>>> RCPT TO:<user@companyB.com>

250 user@companyA.com... Recipient ok

>>> DATA

354 Enter mail, end with "." on a line by itself
```
