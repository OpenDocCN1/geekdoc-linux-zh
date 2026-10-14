
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
[/content]

Wait that's example. Need actual text.

Let's produce correct output.

[content]
- 如果 `AUTHORIZATION` 设置为 "BY"，则以用户 internal 登录时不需要密码。这在开发期间可能没问题，但你可能想在生产系统中提高安全性。若要在以 internal 登录时输入密码，请将 `DBA_AUTHORIZATION` 设置为``（一个空字符串）。

- 如果你的系统有多个数据库实例，你可能希望将默认数据库设置为特定实例。你可以通过 `ORACLE_SID` 值指定此项。Oracle 在安装时将其设置为 `ORCL`（默认数据库）。

- 你还可以将 `ORACLE_HOME` 设置为你喜欢的任何目录。对于桌面版，Oracle 将此配置设置为 `C:\Oracle`（取决于 Oracle 安装在哪个驱动器）。

如需更多性能优化建议，请参阅本书第 16 章“性能优化基础”。

# 图 B.11

Oracle 性能监控器

![](img/563fad4219fcb3a5c1f1e5cc91d831ce_1060_0.png)

# 从 Oracle Windows NT 中学习

我经常发现，最有价值的信息是从以往经验中学到的。在接下来的章节中，我列出了我在 Windows NT 上使用 Oracle 的一些个人遭遇和挣扎。

## 了解局限性

意识到可能影响数据库设计的任何局限性都是重要的。Oracle 经常将这些信息放在晦涩的地方，为了方便，我添加了我遇到的一些限制：

- Windows NT 版 Oracle 8.1.x 的最大 `DB_BLOCK_SIZE` 为 32KB。
- Windows NT 版 Oracle 8.1.x.x 中，任何区段（初始、后续、优化等）的最大尺寸都小于 2GB。

## 安装企业管理器

在服务器上安装企业管理器时（请注意企业管理器主要用于远程管理），确保你的 Windows NT 服务器已安装了 TCP/IP。如果你没有安装 TCP/IP，请设置为 `NETBUI` 并确保 Oracle 的 Bequest 使用唯一的别名进行标识。

## 在 Windows NT 上访问大文件

Oracle 能够绕过 Windows NT 访问大于 4GB 的文件。然而，你需要注意，Windows NT 提供的备份工具在备份这些文件时会遇到最大的困难。你可能需要获取第三方软件包包（如 Seagate、Arserve 等）进行备份，或者你可以创建几个小文件来代替那个大文件。

## UTL FILE 包

`UTL_FILE` 包最初在 Oracle 数据库 7.3.x 版本中引入。该包提供了 PL/SQL 程序访问文件并向其写入输出的能力。它还有自己的错误处理和调试。`UTL_FILE` 包在安装时不会自动安装到系统中，但脚本包含在 Oracle 8.1.x 中，可以在 `ORANT\ADMIN` 目录中找到。该包的文档可以在《Oracle 8 Server: Application Developer's Guide》中找到，它是 Oracle 服务器文档的一部分提供的。

如果你选择使用此包，请确保将目录名称放入 `INITSID.ora` 文件中。这一要求确保了访问文件时的安全性。若要在参数文件中设置目录（你可以放入多个目录），请使用以下格式：

`UTL_FILE_DIR = directory name`

确保目录名称不以 `/` 结尾，因为这会导致 `UTL_FILE.INVALID-PATH` 错误。同时，确保在 `UTL_FILE` 目录中赋予 Oracle 所有者权限，以防止覆盖系统文件带来的风险。记住，为了让数据库识别 `INITSID.ora` 文件中的任何更改，必须关闭并重启数据库。

以下示例代码显示了如何向文件写入消息：

```sql
DECLARE
  al UTL_FILE.FILE_TYPE;
  linebuffer VARCHAR2(80);
BEGIN
  al := UTL_FILE.FOPEN(NULL,'C:\LOG','proc.log','w');
  linebuffer := 'SUCCESS COMPLETION '||TO_CHAR(SYSDATE,'mm/dd/yyyy hh:mi:ss'):')';
  UTL_FILE.PUT_LINE(al,linebuffer);
  UTL_FILE.CLOSE(al);
END;
```

`UTL_FILE.GET_LINE` 的最大缓冲区大小为 1023 字节。尽管如此，至少在 Windows NT 上，可以使用 `UTL_FILE` 包跨网络写入文件。这已被报告为一个问题，且目前尚无解决方法。希望以上信息能为你提供未来可以使用的知识，即使现在还用不上。记住，没有任何软件是无懈可击的。

## 支持 Oracle Windows NT

Windows NT 上的 Oracle 8 版本承诺通过增大其许多限制来使数据库更具企业化。对 Oracle7 的支持将至少持续到 1999 年 12 月 31 日（这是根据 Oracle 世界客户服务 Randy Baker 于 1997 年 8 月的公告）。截至 1997 年 9 月，数据库 8.05 版本是 Windows NT 平台的最新发布。

## 修改回滚段的权限

`ALTER ROLLBACK SEGMENT` 权限, 426

- 应用代码、性能调优以及 244
- `AQ` (高级队列), 207-209
- `ALTER SESSION` 权限, 427
- 应用开发, `SQIJ`, 217
- `ARCH` 后进程, 87
- `ALTER SNAPSHOT` 权限, 427
- 应用目录, `OFA`, 100-101
- 架构师，系统, 127 架构, 56-79
- `ALTER` 语句, 427
- 应用层, `OAS`, 834-836
- 灵活，设计, 98-105 HTTP 监听器层, `OAS`, 841
- `ALTER SYSTEM` 权限, 427
- 应用分区，分区式数据库, 935-938
- 实例架构, 76-100 `MTS` (多线程服务器), 821-822 多线程, `WRB` 和 `Net8`, 789-790
- `ALTER TABLE` 权限, 428
- 应用服务器层, `OAS`, 845-869
- 组件, 847-848
- `ICX`, 851-862
- `OFA` (最优灵活架构), 98-105
- `SQL*Net`, 789-792
- `ALTER TABLE` 语句, 155-156
- `IPC` 支持, 847
- `Jw` 模块, 864-868
- `PL/SQL` 模块, 848-850
- 归档日志, 484-486
- `ALTER TABLESPACE` 权限, 428
- `ARCHIVELOG` 模式, 444
- 归档进程, 87, 95
- `ALTER TABLE` SQL 命令, 66
- 应用系统, `Designer`, 764
- 归档备份工具, 444
- 日志目录，备份, 461
- 重做日志, 461
- `ALTER USER` 权限, 429
- 备键, 18
- 应用调优, 258
- 算术运算符, `PL/SQL`, 601
- 规模分析, 34
- 事务, 33-34
- 索引异常，索引使用以及 272-274
- 查询重写, 277-278
- `SQL TRACE`, 267-270
- 取回缓冲区大小, 692
- 分析阶段，生命周期, 124
- 分析阶段, `SDLC`, 740
- `ANALYZE ANY`, 425
- 数组 `PL/SQL`, 620-622
- `ANSI` (美国国家标准协会), 790
- `ANSI`, `PL/SQL` 以及 588
- `ASO` (高级安全选项), 190-191, 810-833
- `APIs` (应用程序接口) `Designer` 以及, 772-774
- 身份验证, 816-818
- 校验和, 816-818
- `DCE`, 816
- `ICX` 方法, 853
- `Logger API`, `WRB`, 862-864
- `Net8`, 192
- `WRB`, 850-851
- `RADIUS`, 协议支持, 816-818
- `SSL` 以及, 850
- `SSO` 和钱包, 820-821
- 小程序, `OEM`, `Net8`, 188, 191
- 应用独立性，规范化，以及 26
- 应用程序, 833
- 应用，定义, 740
- 创建系统, `Designer`, 749
- 数据库设计, `PL/SQL` 以及 595
- 从 `Designer` 生成, 777-780
- `Java`, `OAS`, 864-868
- 分段, 241-242
- 资产，数据库,
- 监控, 431-434
- 审计，管理, 434
- 审计数据库操作, 432-433
- 审计数据库对象 ML, 433
- 审计登录, 432
- 分配表空间, 424
- 分配, `PL/SQL`, 627-628
- 异步 I/O, `UNIX`, 1013
- 异步传播，复制, 982-983
- 原子事务,
- 属性, 22
- 游标, 632-633
- 标识符, 24
- 命名，关系型表, 16
- 面对象技术, 178
- 对象, `REG`, 18
