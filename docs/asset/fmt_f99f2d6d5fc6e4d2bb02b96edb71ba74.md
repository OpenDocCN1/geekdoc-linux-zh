
`directory mode = 0700`

`locking = no`

[netlogon]

`comment = NT 网域 netlogon 服务共享`

`path = /export/smb/netlogon`

`writeable = no`

`gest = no`

`# logon script = scripts\%U.bat`

`# 如果你想使用脚本，请取消上述行的注释`

`# 别忘了创建它！`

[work]

`comment = 测试者的部门工作目录`

`path = /export/work`

![](img/166cd29830b01a9e3eceb33240be1bcf_384_0.png)

# 第 9 章 网域控制与管理

```
create mode = 0660
directory mode = 0770
write list = @test @research
read list = @test @research
valid users = %S
```

[research]

`comment = 研发组目录`

`path = /export/research`

`create mode = 0660`

`directory mode = 0770`

`write list = @research`

`read list = @research`

`valid users = %S`

[HP]
`comment = HP 激光打印机`
`print command = lpr -r -P%s`
`printable = yes`
`writable = no`
`public = no`

# 将 Windows NT 客户端登录到 Samba 控制的 NT 网域

当前的 NT 网域控制器代码仍在开发中，因此本节旨在作为登录 Samba 控制的 NT 网域的指南。

遵循本章节前面“将 Samba 服务器配置为 Windows 网域的 PDC”中的细节，以便你拥有一个运行正常的 Samba PDC。你需要确认的步骤如下：

- 确保 Samba 服务器在 `smb.conf` 文件中设置了 `encrypted=yes`。
- 在 Samba PDC 上创建必要的机器信任账户，首先在 `/etc/passwd` 中为用户名 `NtClient_workstation$` 创建账户，其中 `NtClient_workstation` 是工作站的 NetBIOS 名称。

> 注意：在当前的 NT 网域控制器代码中，仅使用 UID 来确保 Samba 生成的 `NtClient_workstation` 账户机器 RID（相对 ID）是唯一的。其影响是，即使删除了机器账户，也不应重复使用 `/etc/passwd` 文件中的 UID。机器用户账户设置时不具备普通登录功能且没有主目录，因此使用了 `/etc/passwd` 中的 shell 或主目录字段，并应分别设置为 `/bin/False` 和 `/dev/null`。以下显示了：

```
test1$:*:9008:1000:NT Workstation 1:/dev/null:/bin/false

test2$:*:9009:1000:NT Workstation 2:/dev/null:/bin/false
```

9. 网域控制与管理

360

3. Samba 服务器现在需要创建 `smbpasswd` 账户，因此应使用 `-a -m` 参数调用 `smbpasswd` 命令（`-a` 创建账户，`-m` 表示机器账户）：

```
smbpasswd -a -m NTClient_workstation
```

`/usr/local/samba/private/smbpasswd` 文件将附加机器账户 `smbpasswd` 条目，语法如下：

```
NTClient_workstation:$uid:LM_XXX:NT_XXX[]:LTC-XXXX
```

`LM_XXX` 和 `NT_XXX` 字段分别是 `NTClient_workstation` 密码的 16 字节 LanMan 和 NT 哈希值的 ASCII 表示。

> 注意：如果客户端加入 NT 网域，它最初以其 NetBIOS 名称的小写版本发送密码。成功加入网域后，客户端将使用旧密码作为密钥将其更改为随机值。影响是，如果由于某种原因客户端从网域移除并重新加入，必须在服务器上重置机器信任账户。重新运行 `smbpasswd -a -m` 命令。

如果客户端是 NT 服务器，将需要设置本地登录权限。这可以在网域管理器、策略和用户权限中授予所有人（假设为 NT SP3 或更高版本）本地登录权限。NT 用户将能够本地登录。如果你登录另一个 NT PDC 而不是 Samba PDC，则需要执行此过程。

4. 确认 `smb.conf` 中的 `workgroup` 和 `domain logons` 参数设置正确，所示（对应你的 NT 网域名）：

```
workgroup = SAMBABOOK
domain logons = yes
```

如果尚未设置这些，重启 `smbd` 将创建一个名为 `/usr/local/samba/private/SAMBABOOK.SID` 的文件，权限为 `rw-r--`。该文件包含 Samba PDC 的网域服务器 ID (`SID`)。

文件名的初始部分将来自 `workgroup` 参数的值。该文件是 PDC 和网域的关键标识符，其值对于 PDC 和网域是唯一的。重要的是，如果文件损坏或更改，网域中的机器将无法登录，需要重新创建机器信任账户。

![](img/166cd29830b01a9e3eceb33240be1bcf_386_0)

5. 检查 Samba 服务正在运行（运行 `ps` 查看 `smbd` 和 `nmbd` 服务），因为 NT 客户端现在将尝试登录控制器。在 NT 网络设置对话框中，将网域更改为 `SAMBABOK`。图 9.8 显示了在此处更改。

6. 确认后，NT 客户端将欢迎 NT 网域，如图 9.9 所示。

7. 关闭对话框并允许 NT 客户端重启。

# 获取网域管理器、服务器管理器和策略编辑器

Windows 95 和 Windows NT 的网域管理器、服务器管理器和策略编辑器可以从微软的 FTP 站点 `http://ftp.microsoft.com/Softlib/MSLFILES` 获取。用于 NT 下载的文件名为 `SVRTTOOLS.EXE`，Windows 95 版本名为 `NEXUS.EXE`。

使用正确版本的策略编辑器很重要，虽然 Windows 95 版本可以安装在 Windows NT 上，但它无法编辑 NT 策略文件。NT 服务器策略编辑器 (`poled.exe`) 包含在 NT 服务器光盘中，但遗憾的是没有包含在 NT 工作站中。

![](img/166cd29830b01a9e3eceb33240be1bcf_387_0.png)

图 9.8 更改 NT 网域。

![](img/166cd29830b01a9e3eceb3bcf_387_1.png)

图 9.9 欢迎来到 SAMBABOK 网域。

Windows NT 4 的 Service Pack 3 和 4 包含了 Windows NT 策略编辑器副本。许多杂志光盘中都有 Service Pack 4 的副本。策略编辑器 (`poled.exe`) 以及相关的模板文件 (`*.adm`) 也可用。

Office 97 也可以下载策略模板文件，包括策略编辑器的副本。

# 将 Samba 主机加入 NT 网域

之前的章节处理了由 Samba PDC 控制的 NT 网域的设置。有时也需要将其他 Samba 主机加入网域（由 Samba 控制），就像你可能需要添加任何 Windows 客户端一样。

第一个任务是使用 Samba 服务器的 NetBIOS 名称在 PDC 上创建机器信任账户。可以使用 GUI 服务器管理器或之前的 Samba PDC 过程创建。

创建机器信任账户后，必须停止 Samba 网域上的所有 Samba 服务。使用 `smbpasswd` 程序将机器加入 NT 网域。`smbpasswd` 选项 `-j` 指定你想加入已指定的网域（已识别 PDC NetBIOS 名称），如下所示：

```
smbpasswd -j domainname -r domainPDC
```

Samba 主机将加入 NT 网域，并返回成功结果。

在此示例中，如果 NT 网域名为 `SAMBOOK` 且 PDC NetBIOS 名称为 `SambaPDC`，将看到命令和响应：

```
@sambaclient[root]# smbpasswd -j SAMBOOK -r SambaPDC
smbpasswd: Joined domain SAMBOOK.
@sambaclient[root]#
```
