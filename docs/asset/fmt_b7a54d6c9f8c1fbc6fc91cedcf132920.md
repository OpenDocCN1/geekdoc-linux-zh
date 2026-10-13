
例如，LIDS 可以提供以下保护：

- 无论位于什么文件系统，保护重要的文件和目录不受未经授权的访问，未经授权的 `root` 访问不会让入侵者变成超级用户。
- 保护重要的进程不被任何人终止（包括 `root` 用户）。再次，这减少了 `root` 用户的能力。
- 防止非法程序进行原始 I/O 操作。
- 保护硬盘的主引导记录 (`MBR`)。

LIDS 可以检测到有人使用端口扫描器扫描你的系统，并通过电子邮件通知系统管理员。当 LIDS 发现任何违反规则的行为时，还会通知系统管理员并记录有关违反的详细信息（在 LIDS 保护的不可篡改日志文件中）。LIDS 不仅可以记录并发送关于违反的邮件，还可以关闭入侵者的交互会。

# 构建基于 LIDS 的 Linux 系统

Linux 入侵检测系统 (`LIDS`) 是一个内核补丁和一组管理工具，用于增强操作系统的安全性。`LIDS` 使用引用安全模型，将它引用的一切（主体、对象和访问类型）放在内核中。如果你想了解更多关于这种方法的信息，`LIDS` 项目网站为 `www.lids.org/about.html`。

启用 `LIDS` 的 Linux 系统运行自定义内核，因此你必须从可靠的内核网站（如 `www.kernel.org`）获取最新内核。下载并解压内核到 `/usr/src/linux` 后，下载适用于特定内核的 `LIDS` 补丁。例如，如果你使用内核 `2.4.1`，请确保从 `LIDS` 项目网站下载 `LIDS` 补丁。通常，`LIDS` 补丁和管理工具包命名为 `lids-x.x.x.y.y.y.tar.gz`，其中 `x.x.x` 代表 `LIDS` 版本，`y.y.y` 代表内核版本。

## 第 8 章：内核安全

![](img/6d176ba5e3d859ca2b04a3bba254354c_180_0.png)

在后续的指令中，我针对内核 `2.4.1` 使用 `LIDS 1.0.5`。请根据需要修改版本号。在 `/usr/local/src` 目录下使用 `tar xvzf lids-1.0.5-2.4.1.tar.gz` 命令解压 `LIDS` 源码包。现在你可以对内核进行补丁。

![](img/6d176ba5e3d859ca2b04a3bba254354c_180.png)

确保 `/usr/src/linux` 指向最新的内核源码。你可以简单地运行 `ls -l /usr/src/linux` 查看它指向哪个目录。如果它指向旧版本的内核源码，使用 `rm -f /usr/src/linux` 删除链接，并使用 `ln -s /usr/src/linux-version /usr/src/linux`（其中 `version` 是你下载的内核版本）重新链接。`ln -s /usr/src/linux-2.4.1 /usr/src/linux` 将最新的内核 `2.4.1` 链接到 `/usr/src/linux`。

在可以使用 `LIDS` 之前，你需要对内核源码进行补丁、编译并安装内核。方法如下：

- 1. 以 `root` 身份，在合适的目录下解压 `LIDS` 补丁包。我通常将编译好的源码放在 `/usr/local/src` 目录。同样，从 `/usr/local/src` 目录运行 `tar xvzf lids-1.0.5-2.4.1.tar.gz` 命令。这将创建一个名为 `lids-1.0.5-2.4.1` 的子目录。
- 2. 进入 `/usr/src/linux` 目录并运行 `patch -p /usr/local/src/lids-1.0.5-2.4.1.patch` 对内核源码进行补丁。
- 3. 在 `/usr/src/linux` 目录下运行 `make menuconfig` 启动基于菜单的内核配置。

![](img/6d176ba5e3d859ca2b04a3bba254354c_180.png)

除了使用 `menuconfig` 命令外，你也可以使用 `make config` 命令来配置内核。

- 4. 从主菜单中选择 `Code maturity level` 子菜单，按空格键选择 `Prompt for development/incomplete code/drivers` 退出。
- 5. 在 `General setup` 子菜单中选择 `Sysctl support`；然后退出子菜单。
- 6. 从主菜单中选择 `Linux Intrusion Detection System`（Linux 入侵检测系统）子菜单。

![](img/6d176ba5e3d859ca2b04a3bba254354c_181.png)

- 7. 在 `LIDS` 子菜单中，选择 `Linux Intrusion Detection System support (EXPERIMENTAL)`（NEW）选项。你可以看到选项列表：

  - `(1024)` Maximum objects to manage（最大管理对象数）（NEW）
  - `(1024)` Maximum subjects to manage（最大管理主体数）（NEW）
  - `(1024)` Maximum ACL objects to manage（最大 ACL 对象数）（NEW）
  - `(1024)` Maximum protected objects（最大保护对象数）（NEW）
  - `[ ]` Hang up console when raising a security alert（触发安全报警时挂起终端）（NEW）
  - `[ ]` Security alert when executing unprotected programs before sealing LIDS（密封 LIDS 前执行未保护程序时触发安全报警）（NEW）
  - `[ ]` Try not to flood logs（防止日志泛滥）（NEW）
  - `[ ]` Allow switching LIDS protections（允许切换 LIDS 保护）（NEW）
  - `[ ]` Port Scanner in kernel（内核端口扫描器）（NEW）
  - `[ ]` Send security alerts through network（通过网络发送安全报警）（NEW）
  - `[ ]` LIDS Debug（LIDS 调试）（NEW）

> 对于大多数系统，管理对象、ACL 主体/对象和保护进程的默认限制是足够的。你可以保持默认。如果你如果在用户违反安全规则时让 LIDS 断开终端，请选择 `Hang up console when raising a security alert` 选项。如果你希望在执行程序且 LIDS 保护开启时发出安全报警，请选择 `Security alert when executing unprotected programs before sealing LIDS` 选项。由于 LIDS 在启动期间已启用（如后文所述），你可能会在 LIDS 运行之前运行其他程序。当你选择此项时，也可以 `Do not execute unprotected programs before sealing LIDS` 选项完全禁用未保护程序的执行。除非你完全确定启动期间运行的所有内容（工具和守护进程）都已保护且不会停止正常流程，否则我不建议在启动期间完全禁用未保护程序。

![](img/6d176ba5e3d859ca2b04a3bba254354c_182_0.png)

- 8. 启用 `Try not to flood logs`（NEW）选项。在记录相同条目之间保留默认的 60 秒延迟。这样做可以通过限制日志文件的大小来保护你的系统，并确保日志条目不会写入过快。

![](img/6d176ba5e3d859ca2b04a3bba254354c_182_1.png)

- 9. 如果你想启用切换 LIDS 保护，请选择 `Allow switching LIDS protections`。如果是，你可以通过选择以下选项的值进一步自定义：

  - Number of attempts to submit password（提交密码次数）
  - Time to wait after fail（失败后的等待时间（秒））
  - Allow remote users to switch LIDS protections（允许远程用户切换 LIDS 保护）
  - Allow any program to switch LIDS protections（允许任何程序切换 LIDS 保护）
  - Allow reloading config（允许重新加载配置）

这是我的偏好：

- `[* Allow switching LIDS protections`（允许切换 LIDS 保护）（NEW）
- `(3)` Number of attempts to submit password（提交密码次数）（NEW）
- `(3)` Time to wait after fail (seconds)（失败后的等待时间（秒））（NEW）
- `[* Allow remote users to switch LIDS protections`（允许远程用户切换 LIDS 保护）（NEW）
