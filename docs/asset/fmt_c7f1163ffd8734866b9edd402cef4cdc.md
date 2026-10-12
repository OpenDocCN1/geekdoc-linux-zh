
# 固件运行时更新（PFRUT）

这是如何做到的？目前，升级是在操作系统内部完成的。桌面或服务器随后会重启，此时固件会被传输到主板并刷入 `BIOS` 或 `UEFI`。然而，有一个新的 API 规范，允许固件运行时和遥测（`PFRUT`），这使得无需重启即可刷入固件成为可能。`Intel` 致力于 `PFRUT`（以前称为无缝更新）有一段时间，旨在减少服务器的停机时间。其想法是（热限制）或外部因素的作用（例如，热设计功率的变化）。

`HIFI` 计算 `CPU` 的功率效率和性能，给出核心标值，并与操作系统通信。

这组新补丁正处于修订阶段，必须就它们何时提交到内核（或是否会进入 `5.17` 版本）发布公告。有关此更新的更多信息，请访问 `https://linux.kernel.org/lkmi/2021122015f438.1196-1.ricardo-nero-calderon/linux.intel/`。

# Sysjoker 恶意软件分析

针对 `Linux`、`macOS` 和 `Windows`

第一批 `Sysjoker` 出现于 2021 年 12 月，当时 `Intezer` 的人员正在调查一次针对 `Linux` Web 服务器的攻击。该恶意软件用 `C++` 编写，每个变体都针对其攻击的操作系统进行了专门定制。`VirusTotal` 即使使用 57 种不同的检测引擎也未能检测到该恶意软件。

一旦恶意软件突破防御，它将从 `GitHub` 获取 `Sysjoker` zip 压缩包，解压并执行有效负载。有效负载会收集机器信息，将结果存储并编码在 `JSON` 对象中，连接 `C` 服务器（硬编码的 `Google Drive` 链接）或自身（恶意软件本身），并在受的设备上转发命令。

`Intezer` 为 `Sysjoker` 的每种操作提供了一个指标列表。在 `Linux` 上，文件和服务创建在 `/library/` 目录下，并通过 `cron` 任务 `Reboot` (`/library/Services/updatesysjob`) 创建。如果发现此类 `cron` 任务，务必杀死所有相关进程，手动删除文件和 `cron` 任务，扫描系统以确保所有文件都已删除，并检查可能允许攻击者访问您服务器的任何漏洞。

在 `Intezer` 的初始报告中了解更多关于 `Sysjoker` 的信息（`https://www.intezer.com/blog/malware-analysis/new-backdoor-sysjoker/`）。

# Log4j 漏洞检测

随着 `Log4j` 漏洞持续席扰 `IT` 领域，每个人都在努力防止灾难发生。许多公司和开发团队已经发布了工具来帮助检测和修复漏洞。其中一家公司是 `WhiteSource`。他们新出的 `Log4j Detection` (`https://github.com/whitesource/log4j-detection-distribution`) 是一个开源命令行程序，可扫描您的项目以检测已知的 `CVE`：

- `CVE-2021-45048`
- `CVE-2021-44228`
- `CVE-2021-4104`
- `CVE-2021-45106`

为了让 `Log4j Detection` 正常运行，如果您的项目是 `Gradle` 项目，则需要安装 `gradle`（如果项目是 `Maven` 项目，则安装 `mvn`）。开发者还指出，`Maven` 和 `Bundle` 项目必须在扫描之前进行构建。一旦有了 `Log4j Detection`，可以使用命令 `log4j-detect -d PROJECT`（其中 `PROJECT` 是托管目录）启动扫描。

有关此的更多信息，请确保阅读项目 `README` (`https://github.com/whitesource/log4j-detection-distribution/blob/main/README`)。

# Linux 内核警告级别变革

`Andy Shevchenko`（他并不是一只蝴蝶）某天偶然在 `Linux` 内核邮件列表上评论道：“在何时启用警告级别（`warning-level`），比如 `W=0`，是有意义的？”这引发了全球范围内的变革浪潮。

警告（`warning`）是 `GNU GCC`（`C` 编译器）的一个命令行选项。在编译时，`GCC` 会检测您代码中的错误，将其报告给您，并终止编译代码的尝试。也许您没有犯真正的错误，但代码仍然不是 `C` 语言的良好用法。事实上，`GCC` 会产生警告并继续构建您的可执行文件。也许您正决定将坏警告视为错误。`-error` 选项告诉 `GCC` 这样做。

`Masashi Vanaka` 向 `Andy` 指出，内核添加了新选项。“默认启用警告意味着内核是使用大量新编译器构建的。”

`Andy` 回复说，考虑到 `Masashi` 的反对意见，“`-error` 至少可以保持对更改值的严格控制。”

来自 `Google` 的 `Nick Desaullais` 指出，“`Google` 的内核团队通过创建此类错误来进行免费补丁；这有助于他们保持内核构建的高效。”

所以，这样做至少有一个先例？但 `Nick` 希望这些想法能导致他所在的公司产生定期的补丁。他说：“如果一个构建没有警告，那么很难通过配置来查看你有多少警告，而这些警告并不是轻而易举的。它还让编译器的升级变得困难。如果你有 `Android` 经验，如果人们太忙于适应警告，那么新内核版本添加的新警告就永远被关闭了。内核的经验表明，修复不同的警告也需要不同的时间被接受并进入主线，在此期间构建被破坏了。”

`Linus Torvalds` 也对 `Andy` 关于 `-warning` 的原始帖子做出了回应：“我想这样做，而且很久以前就想这样做，但我们一直依赖编译器在随机版本中不要出现随机警告。”

而且创建一个配置选项效果也不好，因为这意味着如果他们设置了它，就会随机失败，而且如果我们开发出设置了该选项的开发者，这并没有太大帮助。

`End-error` 在受控环境中运行良好。在一般的随机混乱中并非如此。

“尽管如此，我一直积极接受无论是否无条件通过的新警告，然后通过禁用某些编译器和/或选项来处理编译器故障。”

“但那几乎是完美的和平。”

在其他地方，在完全不同的 `Linux` 中，`Cook` 发布了一个补丁，`Linus` 拒绝了，“你不能在不使用它们的情况下添加新警告，这增加了一些极其糟糕的新警告，绝对会掩盖其他警告。”

在随后的帖子中，`Linus` 补充道：“我想在某个时刻启用 `-Warning`，每当我想到它时，结果只是在绕过一个新编译器（或旧编译器）。我们必须调试各种配置（以及代码中的）混乱。”

但随后，`Linus` 通过他自己的邮件回复了自己：“我想要创建一个新的配置选项，将其设置为‘默认是（`y`）’，它适用于任何添加代码构建的人。”

记录者 `Zack Brown` 报告了 `Linux` 内核内部最新的新闻、观点和困境

作者 `Zack Brown`

# Linux 内核开发规模

`Linux` 内核列出了 `Linux` 开发活动的核心。流量极其巨大，每周经常达到 `10,000` 条消息，对于一个人来说，跟上整个开发规模几乎是不可能的。这项任务的少数灵魂之一是 `Zack Brown`。

如果人们有新的编译器或配置仍然有警告，他们可以关闭它，但希望 `Linux` 中的这些警告（或关闭）

为了让 `Log4j Detection` 正常运行，如果您的项目是 `Gradle` 项目，则需要安装 `gradle`（如果项目是 `Maven` 项目，则安装 `mvn`）。开发者还指出，`Maven` 和 `Bundle` 项目必须在扫描之前构建。一旦有了 `Log4j Detection`，可以使用命令 `log4j-detect -d PROJECT`（其中 `PROJECT` 是托管目录）启动扫描。

有关此的更多信息，请确保阅读项目 `README` (`https://github.com/whitesource/log4j-detection-distribution/blob/main/README`)。

如果人们有新的编译器或配置仍然有警告，他们可以关闭它，但希望 `Linux` 中的这些警告（或关闭）

为了让 `Log4j Detection` 正常运行，如果您的项目是 `Gradle` 项目，则需要安装 `gradle`（如果项目是 `Maven` 项目，则安装 `mvn`）。开发者还指出，`Maven` 和 `Bundle` 项目必须在扫描之前构建。一旦有了 `Log4j Detection`，可以使用命令 `log4j-detect -d PROJECT`（其中 `PROJECT` 是托管目录）启动扫描。

如果人们有新的编译器或配置仍然有警告，他们可以关闭它，但希望 `Linux` 中的这些警告（或关闭）

为了让 `Log4j Detection` 正常运行，如果您的项目是 `Gradle` 项目，则需要安装 `gradle`（如果项目是 `Maven` 项目，则安装 `mvn`）。开发者还指出，`Maven` 和 `Bundle` 项目必须在扫描之前构建。一旦有了 `Log4j Detection`，可以使用命令 `log4j-detect -d PROJECT`（其中 `PROJECT` 是托管目录）启动扫描。

如果人们有新的编译器或配置仍然有警告，他们可以关闭它，但希望 `Linux` 中的这些警告（或关闭）
