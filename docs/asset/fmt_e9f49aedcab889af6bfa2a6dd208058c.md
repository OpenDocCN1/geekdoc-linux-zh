
例如，执行 `nss /filewrite=vol1` 将为 `vol1` 卷启用写入复制，但这种影响仅限于最后关闭的文件。

- 集群转移停止文件复制。如果您运行涉及 NetWare 集群的合并项目并在合并期间发生故障转移，文件复制将停止。必须重新运行合并项目。
- 使用 SMS 复制数据。服务器合并工具使用存储管理服务（SMS）作为其文件复制引擎，从 NetWare 服务器复制数据到 OES Linux 服务器。
使用 SMS 可以尽可能保留 NetWare 的信任人权限和文件/目录属性。
- OES Linux 的新 `attrib` 命令。如果您从 NetWare 源服务器复制设置了“删除”属性的文件，则无法使用标准的 Linux 或 Windows 工具从 Linux 目标 NSS 卷上删除这些文件。

Novell 为 OES Linux 提供了一个新的 `attrib` 命令，允许您移除删除属性，并在 Linux 上设置或修改其他支持的 NetWare 属性。更多信息请输入 `attrib -h` 查看在线帮助。
- 创建日期从 NetWare 到 Linux 的变化。从 NetWare 源服务器复制文件到 OES Linux 目标服务器后，这些文件的创建日期将变为今天的日期，而不是文件的原始创建日期。

Linux 文件系统不提供创建日期字段，但 NCP 服务器会显示当前日期。

如果你启用了此项检查，你应该预期会在日志文件中看到许多错误，这是由于 Linux 存储文件系统数据的方式存在固有差异导致的。
- 为服务器合并工具 (SCU) 上的 NCP 客户端启用 UTF-8 编码。你可以使用服务器合并工具从存储双字节字符集（日语、韩语和其他非 ASCII 字符）或扩展 ASCII 字符数据（多国语言）的服务器复制数据。

为了拷贝带有非 ASCII 或扩展 ASCII 字符的数据，你必须在 Windows 2000/XP 的 Novell Client 4.91 中启用 UTF-8 支持，以防止受托者和所有权的丢失。

UTF-8 支持默认关闭。
- 理解 Linux 启用用户的必要性。当你使用服务器合并工具将数据从 NetWare 服务器复制到 OES Linux 上的 NSS 卷时，它会随文件传输 NetWare 受托者权限以及支持的文件和目录属性。

然而，为了保留文件所有权，用户必须启用 Linux 权限（也称为 LUM 启用，因为该过程涉及 OES 中的 Linux 用户管理服务）。

要启用 Linux 或 LUM 权限，必须将一个 eDirectory 用户对象与 eDirectory 组关联。该组对象必须与代表物理 Linux 工作站/服务器的 eDirectory Linux 工作站对象关联。

组对象是必要的，因为 NSS 使用虚拟文件服务 (VFS)，这需要用户 ID (UID) 和组 ID (GID) 来进行授权访问。

# 集成 Linux 版 Novell 企业服务器

有关为 OES Linux 启用 Linux (LUM) 用户的完整细节，请参阅《Novell Linux 用户管理技术指南》(`lumadgd.pdf`)。

该指南可以在 `http://www.novell.com/documentation/oes` 获取，或从你的 3077 课程 CD 中的 `OES_Docs` 目录获取。

- **维护文件所有权信息。** 在将数据从 NetWare 卷拷贝到 OES Linux 上的 NSS 卷时，Novell 建议你在拷贝数据之前通过 LUM 为用户启用 Linux 权限。

如果你在数据拷贝到 OES Linux 服务器后才为用户启用 Linux 权限，文件所有权可能不会立即在目标 NSS 卷上重新建立。

如果你使用 `nuseradd` 命令为用户启用 Linux 权限，用户 ID 将在命令完成后立即更新。

然而，如果你通过 iManager、ConsoleOne 或 `nuseradd` 命令逐个启用用户，用户 ID 可能需要长达四小时才会更新。

你可以在启用 Linux 权限后通过运行 `refresh` 命令来立即触发 ID 更新过程。

有关使用 `nuseradd` 命令的完整细节，请参阅《Novell Linux 用户管理技术指南》(`lumadgd.pdf`) 第 37 页的“`nuseradd`”。

该指南可以在 `http://www.novell.com/documentation/oes` 获取，或从你的 3077 课程 CD 中的 `OES_Docs` 目录获取。

# 准备源服务器和目标服务器

在从服务器合并与迁移工具包启动服务器合并工具之前，你必须通过完成以下步骤准备源服务器和目标服务器：

1. 确保所有源服务器和目标服务器都在运行支持的 NetWare、Linux 或 Windows 服务器软件。

有关支持的 NetWare、Linux 或 Windows 版本的完整细节，请参阅《Novell 服务器合并与迁移工具包》(`scmt11.pdf`) 第 18 页的“支持的源和目标服务器版本”。

该指南可以在 `http://www.novell.com/documentation/oes` 获取，或从你的 3077 课程 CD 中的 `OES_Docs` 目录获取。
2. 如必要，在源和目标 NetWare 或 OES 服务器上应用最新的 NetWare 或 Open Enterprise NetWare 或 (OES) 支持包。
3. 如果在 NetWare 服务器之间进行数据拷贝，请为源服务器和目标服务器设置相同的代码页。

如果两台服务器没有相同的代码页，数据在合并过程中将会丢失。

有关更改服务器代码页的完整细节，请参阅《Novell 服务器合并与迁移工具包》(`scmt11.pdf`) 第 11 页的“更改 NetWare 服务器代码页”。

该指南可以在 `http://www.novell.com/documentation/oes` 获取，或从你的 3077 课程 CD 中的 `OES_Docs` 目录获取。
4. 作为预防措施，你应该拥有目标服务器上所有文件系统和 eDirectory 数据的最新备份。

## 集成 Linux 版 Novell 企业服务器

尽管在数据合并项目期间源数据不会被修改，你仍应该拥有源服务器的最新数据和受托者备份。只有合并打印机时数据才会发生变化。

5. 对于 NetWare/eDirectory 合并，在源和目标 NetWare 服务器上加载最新的存储管理数据请求器 (`smdr.nlm`) 和目标服务代理 (`tsafs.nlm`) 模块。

要加载随 NetWare 操作系统软件提供的 SMS 模块，请在服务器命令行提示符输入 `load smdr` 和 `load tsafs`。
6. 如果你将数据合并到 OES Linux 服务器，请在 shell 提示符输入这些命令在 Linux 上加载模块：

```
/etc/init.d/novell-smdr start

/opt/novell/sms/bin/smsconfig -l tsafs
```
