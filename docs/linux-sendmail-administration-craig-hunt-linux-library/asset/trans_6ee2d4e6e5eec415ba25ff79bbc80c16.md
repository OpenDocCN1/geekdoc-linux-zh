

# 第 3 部分 高级配置 177

- 第 7 章 sendmail.cf 文件 . . . . . . . . . . . 179
- 本地信息部分 (Local Info Section) . . . . . . . . . . . 180
- 定义宏命令 (Define Macro Command) . . . . . . . . . . . . 182
- 定义类命令 (Define Class Command) . . . . . . . . . . . . 186
- 从文件加载类变量 . . . . . . . . . . . 190
- 键值文件命令 (Keyed File Command) . . . . . . . . . . . . . 191
- 版本级命令 (Version Level Command) . . . . . . . . . . . . 197
- 选项部分 (Options Section) . . . . . . . . . . 199
- 消息优先级部分 (Message Precedence Section) . . . . . . 201
- 受信用户部分 (Trusted Users Section) . . . . . . . . . 202
- 报头格式部分 (Format of Headers Section) . . . . . . . 203
- 重写规则部分 (Rewriting Rules Section) . . . . . . . 204
- 传输器定义部分 (Mailer Definitions Section) . 205
- M 命令. . . . . . . . . . . . 207
- 编辑 sendmail.cf 文件 . . . . . . . . . 211
- 测试你的新配置 . . . . . . . 212
- 命令总结 . . . . . . . . . . . . . . 215
- 总结 (In Sum). . . . . . . . . . . . . . . 217
- 第 8 章 理解重写规则 . . . 219
- 基础规则集 (Basic Rulesets) . . . . . . . . . . . . . 219
- 更多规则集 (More Rulesets) . . . . . . . . . . . . . 221
- 传输器规则集 (Mailer Rulesets) . . . . . . . . . . . . . 224
- 重写规则 (Rewrite Rules) . . . . . . . . . . . . . . 226
- 模式匹配 (Pattern Matching) . . . . . . . . . . . 226
- 转换地址 (Transforming the Address) . . . . . . . . . . 231
- 特殊规则集 0 重写规则 242
- 传输器三元组变化 (Mailer Triple Variations).. . . 244
- 总结 (In Sum).. . . . . . . . . . . . . . . 246
- 第 9 章 特殊 m4 配置 . . 247
- 使用 DOMAIN 文件 . . . . 248
- 地址伪装 (Address Masquerading).. . . . . . . . . . . . . . . 249
- 启用伪装 (Enabling Masquerading) . . . . . . . . . . . . 249
- 伪装选项 (Masquerade Options) . . . . . . . . . . . . . . . 251
- 伪装用户名 (Masquerading Usernames) . . . . . . . . . . . . . . . 256
- 编写本地规则 (Writing Local Rules) . . . . . . . . . . . . . . 258
- 配置中继客户端 (Configuring a Relay Client).. . . . . . . . . 261
- 总结 (In Sum) . . . . . . . . . . . . . . . . . . 265

# 第 4 部分 维护健康服务器 267

- 第 10 章 测试 Sendmail 269
- 简单命令行选项 (Simple Command-Line Options) . . . . . . 269
- 使用 -bv 选项 . . . . . . . . . . . 270
- 在详细模式下运行 (Running in Verbose Mode) . . . . . . . . 271
- hoststat 命令 . . . . . 273
- mailq 命令 . . . . . . . . . . 276
- 在测试模式下运行 Sendmail (Running Sendmail in Test Mode) . . . . . . 280
- 使用 /parse 命令测试 (Testing with the /parse Command) . 283
- 处理特定地址类型 (Processing a Specific Address Type) . 284
- 使用 /try 命令测试 (Testing with the /try Command) . 285
- 显示和设置内部规则 (Displaying and Setting Internal Rules) . 287
- 使用调试级别 (Using Debug Levels) . . . . . . . 293
- 总结 (In Sum) . . . . . . . . . . . . . . . . . 298
- 第 11 章 停止垃圾邮件 299
- 不要成为垃圾邮件源 (Don't Be a Spam Source) . . . . . 299
- 定义可接受使用策略 (Define an Acceptable Use Policy) . 300
- 运行识别守护进程 (Run the Identification Daemon).. . . 300
- 正确配置邮件中继 (Properly Configure Mail Relaying) . . 301
- 使用 Sendmail 拦截垃圾邮件 (Use Sendmail to Block Spam). 305
- 使用实时黑洞列表 (Using the Realtime Blackhole List).. . . 306
- 使用 access 数据库 (Using the access Database) . . . . . 309
- 使用反垃圾邮件重写规则 (Using Anti-Spam Rewrite Rules) 312
- 在传输器处过滤垃圾邮件 (Filtering Out Spam at the Mailer) . . . . . . . . . . . . . . 314
- 使用 procmail 管理邮件 (Managing Mail with procmail).. . . . . . . . . . . . . . 315
- 总结 (In Sum).. . . . . . . . . . . . . . . . . . . . . 319
- 第 12 章 Sendmail 安全 . . . . . . . . . . . . . . 321
- 基础安全 (Basic Security) . . . . . . . . . . . . . . . . . . 322
- 硬件安全 (Secure the Hardware) . . . . . . . . . . . . . . . . 322
- 软件安全 (Secure the Software).. . . . . . . . . . . . . . . . . . 324
- 限制登录访问 (Limit Login Access) . . . . . . . . . 328
- 安全 Sendmail 服务器 (Securing a Sendmail Server) . . . . . . 335
- 防止未经授权访问 Sendmail (Securing Sendmail against Unauthorized Access) . . 337
- Sendmail 安全协议 (Sendmail Protocols) . . . . . . 342
- 加密与密码学 (Encryption and Cryptography) . . . . . 343
- Sendmail 身份验证 (Sendmail Authentication) . . . . . 344
- 传输层安全 (Transport Layer Security) . . . . . . . 350
- 总结 (In Sum).. . . . . . . . . . . . . . . 356

# 附录

- 附录 A m4 参考 (Appendix A m4 Macro Reference) . . . . 361
- 完整命令参考 (Complete Command Reference) . . . . . . . 366
- define . . . . . . . . . . . . . . . . 367
- FEATURE . . . . . . . . . . . . . . . 376
- OSTYPE. . . . . . . . . . . . . . . . 382
- DOMAIN . . . . . . . . . . . . . . 388
- DOMAIN . . . . . . . . . . . . . . 388
- MAILER . . . . . . . . . . . . . . 390
- Local Code . . . . . . . . . . . . . . 392
- DAEMON_OPTIONS. . . . . . . . . . . . . . 395
- 本地路由 (Local Routing) . . . . . . . . . . . 395
- 附录 B Sendmail 命令 (Appendix B The Sendmail Command) . . . . . . . . 395
- 命令行开关 (Command-Line Switches).. . . . . . . . . . 396
- 调试级别 (Debug Levels) . . . . . . . . . 399
- 附录 C Sendmail 变量、选项和标志 (Appendix C Sendmail Variables, Options, and Flags) . . . 411
- 变量 (Variables) . . . . . . . . . . . . . . . . . 411
- 类变量 (Class Variables) . . . . . . . . . . . . . . . . 416
- 选项 (Options) . . . . . . . . . . . . . . . . 418
- 传输器标志 (Mailer Flags) . . . . . . . . . . . . . . . . 421
- 索引 (Index) . . . . . . . . . . . . . . . . . 435

