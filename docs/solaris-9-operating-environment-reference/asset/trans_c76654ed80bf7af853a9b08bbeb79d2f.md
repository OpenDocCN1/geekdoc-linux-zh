

# zipinfo 1599

以下示例显示了当环境变量设置为关闭总计行时，如何显示完整的短格式列表。请注意，你必须显式指定 `-s` 选项，因为 `-t` 选项本身意味着只打印总计行。

```
castle$ setenv ZIPINFO --t
castle$ zipinfo -t 085XDOCS
4 files, 302592 bytes uncompressed, 105858 bytes compressed: 65.0%
castle$ zipinfo -st 085XDOCS
Archive: 085XDOCS.zip 106272 bytes 4 files
-rw-a-- 2.0 fat 76800 t-defn 18-Aug-98 21:55 085X1.DOC
-rw-a-- 2.0 fat 67072 b-defn 22-Aug-98 01:39 085X2.DOC
-rw-a-- 2.0 fat 95232 t-defn 31-Aug-98 20:29 085X42.DOC
-rw-a-- 2.0 fat 63488 t-defn 4-Oct-98 20:24 085X4E.DOC
4 files, 302592 bytes uncompressed, 105858 bytes compressed: 65.0%
castle$
```

`-s` 选项列出 `-mand` 和 `-l`，默认包含头部和标题，除非另有指定。由于指定的环境变量未指定总计行，且该设置的优先级高于 `-s` 的默认行为，你必须使用显式的 `-t` 选项来生成完整列表。由于没有对头部进行任何说明，`-ts` 选项就足够了。

以下示例详细列出了包内单个文件的详细信息。

```
castle$ zipinfo -m 085XDOCS1.DOC
-rw-a-- 2.0 fat 76800 -64% defN 18-Aug-98 21:55 085X1.DOC
castle$
```

当你使用任何格式选项指定任何单个文件时，`zipinfo` 只会显示有关请求文件的单行信息，无论头部和标题的默认规范如何。你也可以在命令中添加 `-t` 选项。

以下示例使用详细选项并将输出通过给 `more(1)` 命令，显示了该 zip 压缩包的第一屏屏幕信息。

```
castle$ zipinfo -v 085XDOCS | more
Archive: 085XDOCS.zip 106272 bytes 4 files
```

中央目录结束记录（End-of-central-directory record）：

```
Actual offset of end-of-central-dir record: 106250 (0001F0Ah)
Expected offset of end-of-central-dir record: 106250 (0001F0Ah)
(基于中央目录长度及其（预期）偏移量)
```

此 zip 文件构成单部分存档的唯一磁盘；其中央目录包含 4 个条目。中央目录长度为 226 (00000E2h) 字节，其从 zip 文件开始的（预期）字节偏移为 106024 (00019E28h)。

没有 zip 内容。

中央目录条目 #0：

# zipinfo

085X01.DOC

| 字段 | 值 |
| :--- | :--- |
| 本地头部相对于存档开始的偏移量: | 4 (00000004h) 字节 |
| 源文件系统或操作系统: | MS-DOS, OS/2 或 NT FAT |
| 编码软件版本: | 2.0 |
| 要求的最小文件系统兼容性: | MS-DOS, OS/2 或 NT FAT |
| 所需的最小软件版本: | 2.0 |
| 压缩方法: | deflated |
| 压缩子类型 (deflation): | normal |
| 文件安全状态: | 未加密 |
| 扩展本地头部: | 无 |
| 文件最后修改时间 (DOS 日期/时间): | 1998年8月18日 21:55:14 |
| 32位 CRC 值 (十六进制): | dcd305ce |
| 压缩大小: | 28048 字节 |
| 解压缩大小: | 76800 字节 |
| 文件名长度: | 10 个字符 |

--

以下示例展示了使用 `zipinfo` 中的 `-T` 选项配合 `sort(1)` 和 `tail(1)` 命令，显示存档中最近修改的文件。

```
castle$ zipinfo -T 085XDOCS sort -n +6 | tail -15
Archive: 085XDOCS.ZIP 106272 bytes 4 files
--rw-a 2.0 76800 b-def 19990818.215514 085X01.DOC
--rw-a 2.0 67072 b-def 19990822.013496 085X02.DOC
--rw-a 2.0 95232 t-def 19990831.202906 085X02.DOC
--rw-a 2.0 63488 t-def 20240104.204202 085X04.DOC
--rw-a 2.0 50688 b-def 8-Jan-99 09:48 085X08.DOC
--rw-a 2.0 73238 t-def 1998-Dec-14 18:18 085X19.ELF
6 files, 44314 bytes uncompressed,1439 bytes compressed:67.4%
```

`-T` 选项配合 `sort(1)` 按 ASCII 顺序排序。`+6` 选项在第一个字段之后排序（即第七个字段）。这被视为默认格式列表；`tail(1)` 命令过滤掉除了最后 15 行。`zipinfo` 可能将日期/时间作为内置选项。

要使用星号显示文件列表，你必须在其前面加上反斜杠进行转义。以下示例显示了关于三个存档的信息。

```
castle$ zipinfo *.ZIP
Archive: 085DOCS.ZIP 145031 bytes 6 files
--rw-a 2.0 76800 b-def 18-Jan-99 21:55:15 085X01.DOC
--rw-a 2.0 67072 b-def 22-Aug-98 03:19 085X02.DOC
--rw-a 2.0 80384 b-def 24-Sep-98 18:40 085X03.DOC
--rw-a 2.0 95232 t-def 19-Aug-98 20:29 085X04.DOC
--rw-a 2.0 50688 b-def 8-Jan-99 09:48 085X08.DOC
--rw-a 2.0 73238 t-def 1998-Dec-14 18:18 085X19.ELF
6 files, 150038 bytes uncompressed,43099 bytes compressed:71.3%
```

# zipinfo

成功处理了两个存档。

# 另请
ls(1), unzip(1)

# URL
Info-ZIP 主页当前位于：http://www.cdrom.com/pub/infozip

# 版权
经 Info-ZIP 许可发布。请访问 http://www.cdrom.com/pub/infozip/doc/COPYING 获取版权信息。

# 作者
Greg "Cave" Roofs。ZipInfo 包含了 Mark Adler 的模式匹配以及许多人的改进。请参考源码获取更完整的列表。

# Prentice Hall: 专业技术参考
为今天的专业人士提供未来的解决方案。

# 与 PTR Online 保持同步！
我们努力处于专业计算机科学和工程的前沿。当你访问 www.phptr.com 时，可以发现以下内容：

- 特殊兴趣领域，提供我们最新的书籍、丛书、本月特色、相关链接以及帮助你完成工作的其他信息。
- 优惠，优惠！来到我们的促销板块，获取零售商独家提供的最新折扣。
- 需要寻找书店吗？你附近可能有出售多种 PTR 书的书店。在 www.phptr.com 查找书店。
- PTR 有什么新鲜？我们不仅为专业社区出版书籍，我们也是他们的一员。查看我们的日程，加入作者聊天，获取感兴趣主题的最新评论和新闻稿。
- 立即订阅！加入 PTR 的月度电子邮件通讯！
想获取你感兴趣区域的最新动态吗？在我们的网站上选择一个目标类别，我们将让你了解你所在地区的 PTR 产品、作者活动、评论和会议。

立即访问我们的邮箱箱进行订阅！http://www.phptr.com/mail_lists

![](img/185d23104c385dfb6a62d4cc96b8997_1633_0.png)

# 来自你熟悉并信任的专家 IT 解决方案。
文章 免费库 专家问答与培训中心 下载 我的InformIT

登录 注册 关于InformIT

# 主题
操作系统
Web 开发
编程
安全
认证
在线

# www.informit.com
- 免费、深入的文章和补充材料
- 在需要时掌握你所需的技能
- 从行业领先的籍、电子书和培训产品中进行选择
- 在需要时获取答案——来自现场专家或 InformIT 的综合库
- 获取行业认证并提升你的职业

# 专家访问

![](img/185d23104c385dfb6a62d4cc96b8997_1634_0.png)

立即访问 InformIT，获取来自 PH PTR 的优质内容
免费内容
Prentice Hall / 版权所有 2000 Pearson

