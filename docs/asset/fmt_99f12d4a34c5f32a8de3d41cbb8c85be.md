
> **重要：** 在某些情况下，`pam_mount` 模块无法设置 setuid root，这意味着普通的 `mount` 命令失败并返回“only root can do that”的错误。然而，这种情况正在变得越来越少。

从域挂载共享时一个可能的问题是，`pam_mount.conf` 文件中的特殊字符 `&` 会扩展为整个用户名，包括域名名和 windbind 分隔符。最好的做法是在使用 `pam_mount` 时配合 `smb.conf` 文件中的 `windbind default domain = yes` 选项，以获取不带域名和 windbind 分隔符的用户名。否则，需要额外的脚本在执行挂载之前删除用户名中的这部分内容。

> **提示：** 使用 `pam_mount` 时，请为域用户使用简单的用户名。这意味着按照第 199 页 9.2.1 节“windbind 的通用实现”所述设置 `default domain` 选项。

## 9.6.2 Novell Linux Desktop pam_mount

在 Red Hat Desktop 中使用 Novell Linux Desktop 和 `pam_mount` 的情况略有不同。最新版本的 `pam_mount` 可以在 Novell Linux Desktop 中编译。然而，在 `sshd` 中使用 `pam_mount` 似乎极其困难。

`Pam_mount` 被添加到 `/etc/pam.d` 中所有需要自动挂载的服务文件中。该模块由“auth”认证部分通过 PAM 获取密码和执行实际挂载的“session”会话部分组成。因为这是一个会话模块，它可以在会话关闭时卸载文件系统。

> **重要：** 由于某些版本的 OpenSSH 将身份验证拆分为独立的进程，因此密码无法从 `npam_mount` 的 auth 部分传递到 `pam_mount` 的 session 部分。这意味着在这些情况下 `pam_mount` 无法工作。

需要添加的行如下：

```
auth        required        pam_mount.so
```

以及：

```
session optional pam_mount.so
```

`auth` 行应该放在 `pam_unix` 和 `pam_winbind` 行之前。`session` 行应该放在 session 部分。记住在每行 auth 行后添加 `use_first_auth` 参数；否则，`pam_mount` 行将触发第二次密码提示。

`pam_mount` 模块有它自己的配置文件 `/etc/security/pam_mount.conf`。该文件包含此类设置，例如挂载命令所在的位置、调试设置、应该创建哪些挂载点，以及为哪些用户挂载哪些文件系统。用于挂载 SMB 共享的最小 `pam_mount.conf` 文件类似于第 217 页的示例 9-23。

### 9.7 如何在域中使用网络打印机

能够使用现有打印机是任何环境中新类型客户端最重要的前提条件之一。我们不希望为种类型的客户端保留单独打印环境。这意味着 Linux 客户端必须使用域内可用的网络打印机。我们可以通过两种方式实现这一点：

- 使用网络接口直接打印到打印机。
- 使用 Windows 打印服务器及其 SMB 接口打印到打印机。

Linux 客户端使用 CUPS 时可以使用这两种选项。然而，我们建议使用第二种方案，因为域内的所有打印以及用户环境都是平等的。这意味着只有打印任务，而不是 Windows 打印和 Linux 打印。你需要在 Linux 客户端上运行 CUPS。通过以下命令检查：

```
/etc/init.d/cups status
```

这应该返回 CUPS 正在运行并给出其 PID。如果不是，请使用以下命令启动：

```
/etc/init.d/cups start
```

确保 CUPS 在下次启动时自动启动：

```
chkconfig on
```

你还需要确保 CUPS 目录中有一个指向 smpool 的链接：

```
# ls -al /usr/lib/cups/backend/smb
lrwxrxrxr 1 root 21 Mar 1 12:34 ../../../bin/smpool
```

你可以通过此命令检查 CUPS 是否支持 smb：

```bash
# lspinfo -v | grep smb
network smb
```

你可以通过两种方式创建打印机：

- 使用 `lpadmin` 命令
- 使用 CUPS Web界面

我们将详细介绍两种方法。

#### 使用 lpadmin 命令创建打印机

你可以从命令行创建打印机。这允许对许多打印机进行脚本化创建。这意味着域打印机的创建可以集成到登录配置文件中，这样用户就不需要在客户端手动创建打印机。

要在命令行创建打印机，我们使用以下命令：

```
lpadmin -p printer1 -E -v smb:Administrator:SMB3LAB26/printer1
```

你需要将字段更改为你域中的名称。第一个打印机是本地名称，第二个是打印共享名称。服务器 SMB3LAB26 是打印共享。如果共享对所有人可用，可以省略用户名和密码。最佳实践是设置位置。使用 `-m` 选项设置位置。

#### 使用 CUPS Web界面创建打印机

你可以通过 CUPS Web界面完成上述操作。按照以下步骤操作：

1. 在浏览器中加载 CUPS 管理界面图 9-2。
2. 然后管理打印机图 9-3。
3. 点击添加打印机图 9-4。
4. 你进入一个输入打印机名称、位置和描述的页面。然后点击继续图 9-5。
5. 在下一页，为打印机选择设备。选择 Samba 并点击继续图 9-6。
6. 在下一页，为打印机选择模型和驱动程序并点击继续图 9-7。
7. 下一个窗口将根据上一个屏幕选择的模型提供更详细的选择。选择正确的项并点击继续图 9-8。

![](img/23b949da14ff7bab8762f0f0361af394_255_0.png)

# 管理员

打印机 1 已成功添加。

> Copyright 1993-2002 Easy Software Products, All Rights Reserved. The Common UNIX Printing System, CUPS and the CUPS logo 是 Easy Software Products 的商标。所有其他商标均为其各自所有者的财产。

图 9-9 CUPS Web 界面打印机添加成功消息

- 9. 您已将打印机添加到 CUPS。请参见第 229 页图 9-10。

![](img/23b949da14ff7bab8762f0f0361af394_256_0.png)

# 打印机

默认目标：printer1

| printer1 | HP LaserJet 系列 CUPSPS v1.1 |
| --- | --- |
| 说明：AD6380 服务器域上的测试打印机 | 位置：虚拟打印机 |
| 打印机状态：空闲，接受作业。 | 设备 URI：smb://smb3lab26/printer1 |

- 打印测试页 | 停止打印机 | 拒绝作业 | 修改打印机
- 配置打印机 | 删除打印机

Copyright 1993-2002 Easy Software Products, All Rights Reserved. The Common UNIX Printing System, CUPS and the CUPS logos 是 Easy Software Products 的商标。所有其他商标均为其各自所有者的财产

**图 9-10** 带有 printer1 的 CUPS Web 界面管理打印机页面

本节中的截图是使用连接到域控制器 smb3lab26 的 Active Directory 域 AD6380 的 Red Hat 桌面客户端创建的。

要测试您使用 **lpadmin** 或 Web 界面添加的打印机，只需打印一个文件，或使用 Web 界面上的“打印测试页”按钮。

> **重要：** 在创建打印机过程中使用用户名和密码会将您的密码暴露在 CUPS 定义文件中。最好使用特殊的打印机用户，或让打印机共享对所有人可用。

第 9 章 集成指南 229 页

# 第 4 部分

# 附录

在本书的第 4 部分中，包含了：

- 附录 A，“233 页：Windows 用户的 Linux 术汇表”
- 附录 B，“255 页：使用企业管理工具”
- 附录 G，“329 页：应用程序移植”
- 附录 F，“321 页：桌面自动化与脚本”
- 附录 E，“313 页：客户端个性化”
- 附录 C，“277 页：使用 Versora Progression Desktop 自动化桌面迁移”
- 附录 D，“289 页：使用 Useful Desktop Multiplier 深度多站计算”

![](img/23b949da14ff7bab8762f0f0361af394_260_0.png)

# Windows 用户的 Linux 术汇表

本附录描述了基础术语。
