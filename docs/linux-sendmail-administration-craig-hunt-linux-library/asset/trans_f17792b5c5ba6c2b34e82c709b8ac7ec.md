

## 456 UUCP_MAILER_MAX 变量 xinetd 配置

UUCP_MAILER_MAX 变量, 127, 132
UUCP_RELAY 变量, 125–126, 264, 386
UUCSMPTP 命令 (m4), 103, 364

视频媒体类型 (MIME), 16
[VirtHost]-类, 162
虚拟域名, 伪装, 252
虚拟邮件域, 161–163
定义, 197
mailertable 特性，用于, 168
virtuser 数据库, 定义, 197
VIRTUSER_DOMAIN 命令 (m4), 162, 365
VIRTUSER_DOMAIN_FILE 命令 (m4), 365
virtuser_entire_domain 功能, 379
virtusable 数据库, 380–381
virtusable 功能, 128, 143, 161–166, 379
构建与测试, 165–166
投递地址定义, 163–166
软件漏洞，跟踪, 324

## V

V (版本级别) 命令, 182, 197–199, 215 *另需参* 类变量
用于邮件投递器的, 120–121
D 命令的, 182
在模式匹配中, 229
在重写规则模式匹配中, 226
sendmail.cf 文件, 296, 411–416
设置与查看, 287–288
厂商网站, 在某处查找 RPM 软件, 62
厂商。*参见* Red Hat

VERB, 222
详细模式
用于 makemap 命令, 173–174
运行 mailq, 278
SMTP (简单邮件传输协议)
在其中, 11–13
用于测试 Sendmail, 271–273
验证命令 (SMTP), 5, 8
[*verify*] 变量, 353–354

版本级别 (V) 命令, 182, 197–199, 215
版本号
Sendmail 对比 sendmail.cf, 91
要设置的 Z 变量, 184
VERSIONID 命令 (m4), 91, 92, 95, 96, 364
在 generic-linux.mc 文件中, 98, 108
version.m4 文件, 91

## W

网站
ab 安全漏洞, 324
关于垃圾邮件者的信息, 311
控制网络访问的封装器, 330–332

## X

X Windows 工具
用于 Sendmail 安装, 68–69
tksys, 55, 55–56
X.400 协议, 32
X.509 证书, 350
xinetd 配置
用于控制网络访问, 332–335
移除守护进程, 从 327

sendmail.cf 中的 XscriptFileSizeBuffer 选项 – Z 变量 457

sendmail.cf 中的 XscriptFileSizeBuffer 选项, 431
XUSR, 22

## Y

YPCOMPAT 数据库选项, 140

## Z

Z 变量, 91, 184

## 第 3 部分 高级配置 177

## 第 7 章 sendmail.cf 文件 179

- 列表 7.1 信息部分 180
- 列表 7.2 sendmail.cf 中的定义宏命令 183
- 列表 7.3 sendmail.cf 中的定义类命令 187
- 列表 7.4 检查类如何被使用 189
- 列表 7.5 从类加载类变量的命令 190
- 列表 7.6 sendmail.cf 中的 K 类命令 196
- 列表 7.7 示例 sendmail.cf 中的 V 命令 199
- 列表 7.8 sendmail.cf 中的示例选项命令 200
- 列表 7.9 标准消息优先级值 201
- 列表 7.10 sendmail.cf 可信用户部分 202
- 列表 7.11 sendmail.cf 中的头部格式 203
- 列表 7.12 sendmail.cf 中投递的邮件代理器 206

## 第 8 章 理解重写规则 219

- 列表 8.1 两个简单的规则集 225
- 列表 8.2 字面量值的内部使用 228
- 列表 8.3 类值的测试 230
- 列表 8.4 无限标记替换测试 232
- 列表 8.5 重写规则的递归性质 234
- 列表 8.6 Sendmail 配置中紧凑循环的结果 236
- 列表 8.7 从规则中调用另一个规则集 237
- 列表 8.8 从 DNS 获取规范名称 238
- 列表 8.9 从重写规则访问数据库 240

## 第 9 章 特殊 m4 配置 247

- 列表 9.1 示例 DOMAIN 文件 247
- 列表 9.2 MASERADE_AS 对 sendmail.cf 的影响 250
- 列表 9.3 MASERADE_AS 的设置 250
- 列表 9.4 伪装测试 253
- 列表 9.5 伪装用户名 257
- 列表 9.6 本地示例配置 259
- 列表 9.7 规则集测试配置 259

## 第 4 部分 维护服务器 267

## 第 10 章 测试 Sendmail 269

- 列表 10.1 检查规则集 300
- 列表 10.2 启用中继 302
- 列表 10.3 状态检查 303
- 列表 10.4 示例状态报告 304
- 列表 10.5 示例 mailq 305
- 列表 10.6 详细模式 mailq 306
- 列表 10.7 选择性处理队列 307
- 列表 10.8 使用规则集处理地址 308
- 列表 10.9 使用 /parse 处理地址 309
- 列表 10.10 用于邮件代理器的 /try 310
- 列表 10.11 设置与查看变量 311
- 列表 10.12 从外部获取信息 312
- 列表 10.13 调试模式查看配置文件 313
- 列表 10.14 调试模式下的设置 314
- 列表 10.15 调试输出 315
- 列表 10.16 调试级别输出 316

## 第 11 章 停止垃圾邮件 299

- 列表 11.1 检查规则集 300
- 列表 11.2 启用中继 301
- 列表 11.3 测试 dnsbl 功能 302
- 列表 11.4 简单的反垃圾规则集 303
- 列表 11.5 检查头部内容 304
- 列表 11.6 示例 procmail 文件 305

## 第 12 章 Sendmail 安全 321

- 列表 12.1 运行 imaps 329
- 列表 12.2 使用 popauth 329
- 列表 12.3 xinetd 服务 330
- 列表 12.4 Red Hat 的 xinetd.conf 331
- 列表 12.5 xinetd.conf 控制 332
- 列表 12.6 身份验证的 SMTP 333

## Linux Sendmail 管理

对所有问题的权威解答

Linux Sendmail 管理是你能找到的最完整、最的 Sendmail 指南。这本书由当今最著名的专家之一编写，将一步一步地教你安装、配置和维护所需的标准和高级技术。

- 理解 Internet 协议及其扩展
- 理解邮件架构和 Sendmail 的角色
- 在 Linux 系统上安装 Sendmail 源或二进制发行
- 使用 m4 语言构建 Sendmail 配置
- 分析和改进 Red Hat Sendmail 配置
- 使用 Sendmail 数据库进行自定义
- 理解 sendmail.cf 文件及其命令
- 理解规则集并使用规则修改地址
- 隐藏用户名和主机名
- 测试和调试 Sendmail 配置
- 控制垃圾邮件
- 安全 Sendmail 服务器
- 使用 Sendmail 加密技术

应对 Sendmail 的挑战

掌握 m4 配置技术

选择并使用帮助服务器的工具

关于作者
Craig Hunt 是 TCP/IP 和 Linux 专家，经常在新World-Interop、ComNet 等其他贸易展览上演讲。他的其他书籍包括畅销的 Linux Network Servers 24seven 和 Linux DNS Administration，均由 Syex 出版。

关于系列
Craig Hunt Linux Library 包含七本书，为 Linux 管理员提供深入的覆盖。主题涵盖 Samba 服务器管理、系统管理、DNS 服务器管理、Apache Web 服务器管理、NFS 和 Automounter 以及 Linux 安全。该系列的每本书都由 Craig Hunt 编写或由其仔细审查，以确保为网络专业人士提供最高质量和最全面的内容。

