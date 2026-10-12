
在运行学习模式时，非常重要的是记住不要使用授予 `root` 账户的管理权限：诸如启动和停止服务、修改用户账户、安装和卸载软件以及编辑系统配置文件等任务应该被避免，否则这些任务将成为 `ACL` 中 `root` 允许的操作。理想情况下，你希望赋予的权限越少越好，以防发生 `root` 级别的攻破。

学习模式通常应使用一天以上（这样每天运行的 `cron` 任务就会被记录）。在此期间后，使用以下命令禁用访问控制（系统会提示你输入管理员密码）：

```bash
# gradm -D
Password:
```

使用 `-o` 标志从日志文件生成 `ACL`：

```bash
# gradm -F -L /etc/grsec/learning.logs -O /etc/grsec/acl
Beginning full learning 1st pass...done.
Beginning full learning role reduction...done.
Beginning full learning 2nd pass...done.
Beginning full learning subject reduction for user root...done.
Beginning full learning subject reduction for user j...done.
Beginning full learning subject reduction for user smmsp...done.
Beginning full learning 3rd pass...done.
Beginning full learning object reduction for subject /...done.
Beginning full learning object reduction for subject /bin/bash
...done.
Beginning full learning object reduction for subject /bin/cat
...done.
Beginning full learning object reduction for subject /...done.
Beginning full learning final pass...done.
```

你可以指定一个不同的文件来写入这些规则，但推荐的方法（如示例所示）是将它们附加到 `/etc/grsec/acl` 中的任何现有列表中。

## 实现 Grsecurity

`Grsecurity` 具有控制用户和网络服务的特性，非常适合用于 `DMZ` 服务器和内部多用户机器。这些功能中的许多在内核中启用后，只需要极少（或不需要）进一步的配置；由于具有自动生成 `ACL` 的选项，实现 `Grsecurity` 的工作量适中。

## 组

`Grsecurity` 最简单（尽管强大）的功能之一是根据用户所属的组来限制用户。在接下来的示例中，我们假设你已经在内核中启用了组限制功能（如前文所述），并使用了建议的默认组 ID。

对于没有特殊要求的普通用户，我们建议默认将他们放在以下组中：

- `1002`（防止运行网络服务）
- `1005`（仅允许在信任目录中运行二进制文件）

可以通过使用 `useradd` 命令配合 `-G <group1,group2>` 切换来实现：

```bash
# useradd pete -g users -G 1002,1005
```

对于初级管理员来说，这可能显得过于严格，你会发现将他们放在 `Grsecurity` 的任何预定义组中是不实际的。对于潜在的问题用户，你可能还想将他们加入 `1007` 组，这会对 `mount` 和 `exec` 等某些系统调用进行记录。

与物理用户未关联的账户（如 `nobody`、`named`、`www` 等）几乎属于 `1005` 组，你还应该尝试 socket 限制组。主 `DNS` 服务器可以安全地拒绝作为网络客户端的能力（`GID 1003`），但辅助 `DNS` 服务器（定期作为客户端从主服务器检索区域传输数据）需要同时具备客户端和服务器能力。`Sendmail` 同时需要客户端和服务器能力，但通过拒绝 `Apache` 的客户端能力应该是可以的，只要启用 `DNS` 查询的日志记录。

## ACL 生成

你需要创建的 `ACL` 数量在很大程度上取决于默认主体 `/` 的限制紧密程度。虽然高度限制的默认主体对安全有益，但它也为单个主体需要更多的例外。

## 访问控制 361

即使对于经验丰富的 `Grsecurity` 用户，我们也建议使用内置的学习模式来创建初始 `ACL`，这一过程我们在本节较早些部分介绍过了。然而，这个自动生成的 `ACL` 不可避免地需要微调，在本节中，我们将使用一个 `sshd` 的 `ACL` 来更仔细地观察这一过程。

在学习模式下运行 `Grsecurity` 几小时后，生成如下 `ACL`：

```
subject /usr/sbin/sshd o {
/bin h
/bin/bash x
/dev h
/dev/log rw
/dev/ptmx rw
/dev/pts
/dev/pts/1 rw
/dev/tty rw
/etc r
/etc/grsec h
/lib rx
/proc h
/proc/1817
/proc/1819
/usr h
/usr/lib/libcrack.so.2.7 rx
/usr/lib/libglib-1.2.so.0.0.10 rx
/var h
/var/empty/sshd
/var/log
/var/log/lastlog rw
/var/log/wmp w
/var/run/utmp rw
/root
-CAP_ALL
+CAP_DAC_OVERRIDE
+CAP_SETGID
+CAP_SETUID
+CAP_SYS_CHROOT
+CAP_SYS_TTY_CONFIG
bind 0.0.0.0/32:0 dgram ip
connect 192.168.9.100/32:53 dgram udp
}
```

# Linux 网络安全

对 `/proc/<number>` 的引用明显特定于特定的守护进程实例，并且每次启动都会变化，因此无法为它们编写有效的规则。相反，我们将三个 `/proc` 语句泛化为：

```
/proc
```

注意我们必须移除 `/proc` 的（隐藏）标记。同样，分配给连接的终端并不总是 `pts1`，因此我们将 `/dev/pts` 规则泛化为如下内容，允许对 `/dev/pts` 目录及其内容进行读写访问：

```
/dev/pts rw
```

目前的 `bind` 语句允许主体绑定到任何接口上的任何端口。假设我们的 `SSH` 守护进程运行在 `TCP/22` 上，我们可以通过重写该规则来收紧：

```bash
bind 0.0.0.0/32:22 dgram ip
```

最后，`connect` 语句列出了主体被允许连接的地址（而不是谁可以连接到主体）。我们自动生成的 `ACL` 显示，主体尝试连接到 `DNS` 服务器（`192.168.9.100/32:53 dgram udp`）。

然而，我们仍然可以做得。我们的示例目前主体模式为 `o`（覆盖继承），但你记得我们在之前讨论主体模式时提到的，还有许多可用模式。我们可以使用 `n` 模式隐藏窥探的进程（别忘记在默认主体中隐藏 `/var/run/ssh.pid`），使用 `A` 模式保护进程共享内存，使用 `T` 模式防止执行木马代码，并启用 `RANDEXEC`。我们的 `ACL` 第一行现在看起来如下：

```
subject /usr/sbin/sshd ohATx
```

模式的顺序并不重要。最后，我们还可以使用之前讨论的资源限制选项，其中有用的是 `RES_CRASH`。通过以下语句，如果 `SSH` 服务器在 60 分钟内两次崩溃，`Grsecurity` 将阻止其再次启动 60 分钟：

```bash
RES_CRASH 2 60m
```

设置其他资源限制需要实验来确定合适的值，并且它们是次要的。

## 9.3 LIDS: Linux 入侵检测系统 (LIDS)

`LIDS` 最初纯粹是一个 `IDS`，多年来已变成一个更通用的安全项目，类似于 `Grsecurity`。最新的 `LIDS` 系列（第 2 版）使用 `LSM` 框架，而之前的版本是独立实现的。

### 安装

`LIDS` 以内核补丁和一组用户态工具的形式提供，均从 `http://www.lids.org/download.html` 获取。与许多其他项目不同，补丁并不

`LIDS` 仅适用于某些内核版本，但它已经针对 `2.4` 和 `2.6` 系列中的几乎每个内核发布了。找到一个与你现有内核兼容的版本（你可能正是因为该内核适合应用其他补丁而选择了它）应该不是什么问题。

## 内核配置

解压 `LIDS` tar 包，进入内核源码目录，并应用 `LIDS` 补丁：
