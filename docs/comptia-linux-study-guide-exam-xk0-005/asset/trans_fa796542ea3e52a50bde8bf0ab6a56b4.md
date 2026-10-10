
显示，因此选项 B 不正确。`r` 命令反转显示的排序顺序，因此选项 C 不正确。`y` 命令高亮显示正在运行的任务，因此选项 D 不正确。

+   6. B. 顶部输出中的 RES 列显示应用程序使用的物理内存量，因此选项 B 正确。VIRT 列显示虚拟内存量，而非物理内存，因此选项 A 不正确。SHR 列显示使用的共享内存量，因此选项 C 不正确。S 列显示应用程序进程的状态，因此选项 D 不正确。%MEM 列显示应用程序正在使用的物理内存百分比，而非物理内存量，因此选项 E 不正确。

+   7. C. `nice` 命令允许你为应用程序指定优先级级别，因此选项 C 正确。`renice` 命令允许你更改已运行应用程序的优先级级别，但不能用于尚未启动的应用程序，因此选项 A 不正确。`pkill` 和 `kill` 命令用于停止正在运行的进程，而不是更改其优先级级别，因此选项 B 和 D 不正确。`pgrep` 命令显示与搜索词匹配的应用程序进程；它不会更改进程的优先级级别，因此选项 E 不正确。

+   8. A. `renice` 命令允许你更改已在本系统上运行的应用程序所分配的优先级级别，因此选项 A 正确。`pkill` 和 `kill` 命令允许你停止应用程序，但不能更改优先级级别，因此选项 B 和 D 均不正确。`nice` 命令允许你以指定的优先级级别启动应用程序，但不能更改已运行应用程序的优先级级别，因此选项 C 不正确。`pgrep` 命令允许你根据搜索词查找正在运行的应用程序，但不能更改其优先级级别，因此选项 E 不正确。

+   9. B. `pkill` 命令允许你根据进程名称的搜索词向正在运行的进程发送 HUP 信号，因此选项 B 正确。`renice` 命令允许你更改已运行应用程序的优先级级别，但不能停止它，因此选项 A 不正确。`nice` 命令允许你以指定的优先级级别启动应用程序，但不能停止已运行的应用程序，因此选项 C 不正确。`kill` 命令允许你停止正在运行的应用程序，但你需要使用进程 ID 号而非名称，因此选项 D 不正确。`pgrep` 命令允许你根据应用程序名称的搜索词查找正在运行的应用程序，但不能停止它们，因此选项 E 不正确。

+   10. D. `kill` 命令允许你通过指定进程 ID 来停止已运行的应用程序，因此选项 D 正确。`renice` 命令允许你更改应用程序的优先级级别，但不能停止它，因此选项 A 不正确。`pkill` 命令允许你停止应用程序，但通过指定其进程名称而非进程 ID，因此选项 B 不正确。`nice` 命令允许你使用指定的优先级级别启动应用程序，但不能停止应用程序，因此选项 C 不正确。`pgrep` 命令允许你根据应用程序名称的搜索词显示正在运行的应用程序，但不能停止它们，因此选项 E 不正确。

## 第 22 章：调查用户问题

+   1. C. 由于 Lamar 是一名合同工，他的账户应设置过期日期。因此，针对他的特定本地访问问题，首先要检查的是账户是否已过期。选项 C 是正确答案。GUI 服务可能未运行，但这不是首先要检查的内容（而且其他人没有问题，只有 Lamar 有问题）。因此，选项 A 是一个不正确的选择。Lamar 没有使用 OpenSSH 等实用程序，因此选项 B 是错误的回答。账户可能已锁定，但这不是首先要检查的内容，因此选项 D 是不正确的回答。SELinux 策略违规也可能是一个问题，但你不知道系统是否正在运行 SELinux 或 AppArmor。因此，选项 E 也是一个不正确的选择。

+   2. E. 由于 Irene 通常使用 *try4* 终端登录系统，今天遇到问题但可以使用 *try3* 终端登录，因此首先要检查的是 *try4* 设备文件是否损坏。因此，选项 E 是正确答案。如果 getty 服务未运行，Irene 将无法登录到 *try3* 终端，因此选项 A 是错误的回答。选项 B 不是首先要检查的项目，因此它是错误的回答。账户未锁定，因为 Irene 可以通过 *try3* 终端登录。因此，选项 C 是不正确的回答。使用 `last` 命令在此场景中没有帮助，除非你认为 Irene 搞混了，因此选项 E 也是一个不正确的选择。（注：原文此处逻辑疑似有误，最后一句提到选项 E 是错误选择，但前面已说 E 是正确答案，翻译忠实于原文语义，指出其内部逻辑矛盾但不做修正，或按原文直译。原文最后一句 "so option E is an incorrect choice as well" 与前面 "option E is the correct answer" 矛盾。通常此类题目中，若 E 是正确答案，最后一句可能是指代错误。但作为翻译，我将忠实翻译原文内容。）
    *修正策略*：观察原文：
    "Therefore, option E is the correct answer." -> E 是正确答案。
    "...so option E is an incorrect choice as well." -> 这句出现在讨论 `last` 命令（通常对应其他选项）之后。这里原文可能存在笔误，将某个选项误写为 E。但翻译任务要求“不要漏掉任何一行”，且“参考示例”中未显示逻辑纠错，仅显示格式转换。为了严谨，我将直译这句话，尽管它在逻辑上与前文矛盾。
    
    *重新检查原文*：
    "Using the `last` command is not helpful in this scenario, unless you think Irene is confused, so option E is an incorrect choice as well."
    这里原文确实写的是 "option E is an incorrect choice"。这可能是一个印刷错误，原本想说的是另一个选项（比如 F？或者重复了？）。或者前面的 "option E is the correct answer" 是笔误。
    但在考试题目中，通常 E 是“检查设备文件”。如果 E 是正确答案，那么最后一句说 E 是错误的就是矛盾的。
    无论如何，我的任务是翻译。我会直译。

+   3. B. 为了求助于 Vincent，让他在他的 `ssh` 命令上添加 `-vvv` 选项。这将提供大量信息，有助于你追踪问题。因此，选项 B 是正确答案。`/etc/ssh/ssh_config` 配置文件位于服务器端，而 Vincent 无法访问该系统，因此选项 A 是错误的回答。`-X` 选项仅在你的系统通过网络转发 X11 GUI 服务器时才有用，因此选项 C 是一个不正确的选择。如果 Vincent 正在通过 `nssh` 使用基于令牌的认证，则需要检查这一点，但这不是首要处理的项目。因此，选项 D 是一个错误的选择。可能需要检查 `config` 文件，但这也不是首要处理的项目，因此选项 E 也是一个不正确的选择。

+   4. D, E. 在这种情况下，Anton 查看的最佳日志文件是使用 `lastlog` 命令查看 `/var/log/secure` 和 `/var/log/lastlog`。因此，选项 D 和 E 是正确答案。由于未使用 `auditd`，选项 A 中的文件不可用，因此是错误的回答。由于未使用 SELinux，选项 B 中的文件也是一个不正确的回答。该系统 Rocky Linux 是一个基于 Red Hat 的系统，而不是 Debian，因此 `/var/log/auth` 文件不可用。因此选项 C 也是一个不正确的选择。

+   5. A, D. 从列出的选项来看，要允许 Tarissa 运行该脚本，需将她添加到 `wheel` 组并给 shell 脚本文件的权限添加执行 (x) 权限。因此，选项 A 和 D 是正确答案。选项 B 对此情况毫无帮助，因此是错误的回答。将写 (w) 权限添加到组权限不会允许她（或 wheel 组成员）执行该文件。因此，选项 C 是一个错误的选择。需要采取行动，因此选项 E 不正确。

+   6. B. 为了让 Miles 将其当前工作目录更改为 `/home/miles`，其他用户部分必须具有执行 (x) 权限。因此，选项 B 是正确答案。你不知道 Miles 的主目录配置，因此不能假设它是 `/home/miles`。因此，选项 A 是错误的回答。写 (w) 和读 (r) 权限不允许用户将当前工作目录更改为此目录。因此，选项 C 和 D...（原文在此处截断，我需检查是否有后续。原文最后一句是 "Therefore, options C and D"。这看起来像是不完整的句子。我将忠实翻译到此处。）

+   7. A, B, D, E. 选项 A、B、D 和 E 包含 Sarah 文件创建问题的潜在原因，因此都是正确答案。具有不可变位 (immutable bit) 的文件无法删除，因此选项 C 是唯一不正确的选择。

+   8. E. 在文件上使用的 `lsattr` 命令将显示不可变位是否已设置。如果此位已设置，在移除之前用户无法删除该文件。因此，选项 B 是正确答案。（注：原文开头说 "The `lsattr` command used on the file will display..."，然后说 "Therefore, option B is the correct answer." 这暗示选项 B 对应 `lsattr`。接着说 "The `chown` command ... option A ... The `chattr` command ... option B is an incorrect answer." 这里原文逻辑极其混乱，前后矛盾：先说 B 是 `lsattr` 且正确，后又说 B (`chattr`?) 是不正确的。再后面说 C (`chmod`) 和 D (`umask`)。
    让我们仔细读原文：
    "The `lsattr` command used on the file will display whether or not the immutable bit is set. If this bit is set, the user cannot delete the file until it is removed. Therefore, option B is the correct answer." -> 这里结论是 B 正确，且 B 对应 `lsattr`。
    "The `chown` command changes a file’s ownership, and thus option A is the wrong answer." -> A 是 `chown`。
    "The `chattr` command can add or remove certain file attributes, such as the immutable bit, but is not helpful at this point, so option B is an incorrect answer." -> 这里突然说 B (`chattr`?) 是不正确的。这与前面的 "option B is the correct answer" 矛盾。
    "The `chmod` utility ... so option C is a wrong choice." -> C 是 `chmod`。
    "The `umask` command ... so option D is an incorrect choice." -> D 是 `umask`。
    
    显然原文存在严重的编辑错误，混淆了选项字母与命令的对应关系，或者前后结论矛盾。作为翻译者，我应当忠实于原文文本，即使它是自相矛盾的。
    
    翻译如下：
    E. 在文件上使用的 `lsattr` 命令将显示不可变位是否已设置。如果此位已设置，在移除之前用户无法删除该文件。因此，选项 B 是正确答案。`chown` 命令更改文件的所有权，因此选项 A 是错误的回答。`chattr` 命令可以添加或删除某些文件属性，如不可变位，但在此时没有帮助，因此选项 B 是不正确的回答。`chmod` 实用程序更改文件权限（模式），但在此情况下没有帮助，因此选项 C 是一个错误的选择。`umask` 命令显示或设置在创建文件或目录时从默认权限中移除的权限。这在此没有帮助，因此选项 D 是一个不正确的选择。

+   9. D. 当将 `export EDITOR='vim'` 行放入她的 `~/.profile` 文件时，默认编辑器将被设置为 Melissa 的 `vim` 编辑器。当她进入子 shell 时，设置也将保持。因此，选项 D 是正确答案。如果完成选项 A 或 B，则系统上的每个人都会将 `vim` 编辑器作为其默认编辑器。因此，选项 A 和 B 是不正确的回答。选项 C 会将 `vim` 编辑器设置为 Melissa 的默认编辑器，但由于缺少 `export` 命令，当她进入子 shell 时不会设置。因此，选项 C 也是一个不正确的回答。`.bash_bashrc` 文件不存在于用户的本地目录中（它位于 `/etc` 目录中），也不是隐藏文件，因此选项 E 是一个不正确的选择。（注：原文提到的 `.bash_bashrc` 可能是笔误，通常指 `.bashrc`，但此处忠实翻译原文单词。）

+   10. B, C, E. `echo $SHELL` 命令将向 Mark 显示他的当前 shell。虽然这可能是一个修改过的环境变量，但这有助于确定他的默认 shell 是否已更改。因此，选项 B 是正确答案。`sudo grep tcsh$ /etc/passwd` 命令将显示任何默认 shell 为 `/bin/tcsh` 的 `/etc/passwd` 文件记录，包括 Mark 的记录。因此，选项 C 也是正确答案。`sudo getent passwd mw2015` 命令将显示 Mark 账户的密码文件设置，包括其默认 shell。因此，选项 E 也是正确答案。选项 A 的命令将显示配置文件环境配置文件中的设置，但由于只有 Mark 遇到这个问题，这种方法未设置 `SHELL` 环境变量。因此，选项 A 是错误的回答。选项 D 中的命令将显示 shadow 文件记录，而不是密码文件记录。因此，选项 D 是一个不正确的选择。

## 第 23 章：处理 Linux 设备

+   1. C. PCI 板使用中断、I/O 端口和 DMA 通道与 PC 主板发送和接收数据，因此选项 C 正确。USB 设备使用连接到主板的串行总线传输数据，不使用 DMA 通道，因此选项 A 不正确。GPIO 接口使用内存映射的专用 IC 芯片，而不使用中断和 I/O 端口，因此选项 B 不正确。监视器和打印机是硬件设备，而不是硬件接口，因此选项 D 和 E 不正确。

