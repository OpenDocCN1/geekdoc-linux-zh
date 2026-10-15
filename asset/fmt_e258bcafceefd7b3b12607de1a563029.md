
#### @()smtp.m4    8.33 (Berkeley) 96/7/9 ####

重要的标志是 `"e"`。如果你的文件中的其他标志看起来不同，请不要担心。保持你的标志原样，仅在需要时使用 `"e"`。

### 2.2.2 使用 m4 源码配置 sendmail.cf

在下文中，为了简单起见，假设 `sendmail` 版本为 8.8。如果你想看新闻，将你的 `nntp` 服务器设置为你 ISP 的新闻服务器。

这就好了，各位，现在一切都应该运行正常了。要连接到你的 ISP，只需以 `root` 身份运行 `/ppp-connect`。然后，以你的身份运行 `fetchmail -a` 来获取邮件。如果你想浏览邮件和新闻，可以使用像 `Lynx` 这样的基于文本的浏览器来上网。将任何意见、问题和建议发送至 mrates@croftj.net

## Linux 邮件队列简易入门指南

Leif Erlingsson, leif@lege.com, Jan P Tietze, jptietze@mail.hh.provi.de v2.02, 1997年9月3日,
`sendmail` 8.8.7

队列远程邮件 + 投送本地邮件：使 `Sendmail` 投送本地邮件的必要配置——**现在**将远程邮件暂存在队列中直到“我发话”为止。

## 目录

- 1 引言
- 2 非拨号按需解决方案部分
  - 2.1 启动 sendmail
  - 2.2 配置 sendmail
    - 2.2.1 直接配置 sendmail.cf 以进行简单配置
    - 2.2.2 使用 m4 源码配置 sendmail.cf
  - 2.3 菜单支持建议
- 3 拨号按需解决方案部分
  - 3.1 配置 sendmail.cf
    - 3.1.1 直接配置 sendmail.cf 以进行简单配置
    - 3.1.2 使用 m4 源码配置 sendmail.cf
  - 3.2 添加拨号延迟
    - 3.2.1 直接配置 sendmail.cf
    - 3.2.2 使用 m4 源码配置 sendmail.cf
- 4 投递邮件
  - 4.1 如何在特殊时间投递邮件

## 1 引言

本文由两位作者编写。非拨号按需解决方案部分（最旧部分）由 Leif Erlingsson<leif@lege.com> 编写，较新的拨号按需解决方案部分由 Jan P Tietze <jptietze@mail.hh.provi.de> 编写。

## 2 非拨号按需解决方案部分

由 Leif Erlingsson<leif@lege.com> 编写。

... 后文

## 非拨号按需解决方案部分

```
#### @()smtp.m4    8.33 (Berkeley) 96/7/9 ####

Msmtp,      P=[IPC],fMDFMUXe, S=11/31, R=21, E=\r\n, L=990,

             T=DNS/RFC8222/SMTP $ 

             A=IPC $

Mesmtp,     P=[IPC],fMDFMUxae, S=11/31, R=21, E=\r\n, L=990,

             T=DNS/RFC8222/SMTP,

             A=IPC $

Msmtp8,    P=[IPC],fMDFMUxe, S=11/31, R=21, E=\r\n, L=990,

             T=DNS/RFC8222/SMTP,

             A=IPC $

nMrelay,     P=[IPC],fMDFMUxa8e, S=11/31, R=61, E=\r\n, L=2040,

             T=DNS/RFC8222/SMTP,

             A=IPC $
```
