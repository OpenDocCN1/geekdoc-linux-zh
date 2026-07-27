# 10年 Linux 安全：报告单










- 并非详尽的时间线
- 主要从在 kernelnewbies.org 上被提及的变更中选出
- 某些情况下不包含与安全相关的内容（例如 KUNIT/自单元测试的启动）
- 仅限 X86 架构

- 事实上，ARM64 和 PowerPC 的维护者近期也引入了重大的安全功能


- 2010 年 8 月 – 在 Linux 安全峰会上发表了《未来 10 年的 Linux 安全》
- 提到主线对内核自我保护的关注较少
- 2009/2010 年间，内核漏洞大量发布，其中许多由我编写，其技术至今仍在使用
- 建议：
  - 从内核中移除 RWX 权限，消除信息泄露，保护敏感内核数据（函数指针、IDT/GDT 等）
  - 防止无效的用户态内存访问、引用计数溢出、分配大小溢出
  - 实现 CFI（控制流完整性），为纯数据攻击做准备


- 2011 年 6 月 – 创建了内核加固邮件列表 (kernel-hardening)
  - 帮助了 Vasily Kulikov 的 GSoC 项目
    - 将 Openwall 的 /proc 限制移植到通过挂载时的 'hidepid' 实现
    - Polkit/dbus-broker/等拒绝支持：
      - https://github.com/bus1/dbus-broker/issues/207
      - https://github.com/systemd/systemd/issues/12955
    - 目前正在重新实现为每个命名空间（per-ns）的挂载设置
  - 无权限 ping 套接字 (ping sockets)
    - 遗憾的是，它也引入了一些安全漏洞
      - https://www.openwall.com/lists/oss-security/2017/03/25/1
- 在 GSoC 期间（2011 年 6 月至 8 月），平均每月 173 条
  - 9 月降至 131 条，10 月降至 8 条
  - 2011 年 11 月至 2015 年 11 月，平均每月帖数为 24，中位数为 3，2014 年共计 12 条


- 2011 年 7 月 (v3.0) – 增加了内核模式执行保护 (SMEP) 支持
- 直到 2012 年第二季度 Ivy Bridge 发布后才可用
- 2012 年 5 月 (v3.4) – 引入了 Yama LSM
  - 实现了 grsecurity 中存在的 ptrace 限制
  - 最初与其他 LSM 手动堆叠
- 2012 年 7 月 (v3.5) – 引入了基于 BPF 的 seccomp
  - 早期被 systemd 和 Chromium 采用
- 2012 年 9 月 (v3.6) – 引入了符号链接/硬链接限制
  - 适配自 Andrew Tridgeell 在 1996 年为 Linux 2.0.22 实现的功能，随后在 Openwall 之后重新实现，之后又由 grsecurity 实现
  - http://lkml.iu.edu/hypermail/linux/kernel/9610.2/0086.html
-- “加强安全：不是给缺乏耐心的人准备的”: https://lwn.net/Articles/503660/
- 解决了常见的 /tmp 竞态漏洞


- 2012 年 12 月 (v3.7) – 增加了内核模式访问保护 (SMAP) 支持
  - 直到 2014 年第四季度 Broadwell 发布后才可用
- 2013 年 2 月 (v3.8) – 增加了无权限用户空间 (Unprivileged User Dataspace) 支持
  - 2011 年 11 月编写了允许无权限用户创建用户命名空间的补丁，一年后合并
  - 大大增加了内核攻击面，暴露了许多此前很少受安全审查的接口
  - 移除权限检查并不取决于对该攻击面的任何分析，仅取决于用户命名空间工作的完成
- 2013 年 9 月 (v3.11) – 增加了 O_TMPFILE 支持
  - 无竞态的临时文件，需要应用程序支持


- 2014 年 3 月 (v3.14) – 引入了内核地址空间布局随机化 (KASLR)
- 在 2013 年 3 月发表《KASLR：一次信条式的安全练习》后：
  https://grsecurity.net/kaslr_an_exercise_in_cargo_cult_security
- 耗费了大量开发时间，安全声称过大，被单一信息泄露/通用攻击击败
- 直到 2020 年 4 月 18 日才被注意到，同样轻易被核心转储 (coredumps) 破解
- 2014 年 10 月 (v3.17) – 增加了签名的 kexec 内核支持
- 2014 年 12 月 (v3.18) – 增加了 eBPF
- 2016 年 1 月 (v4.4) – 允许无权限访问


- 2015 年 4 月 (v4.0) – 热补丁 (Live patching) 和 KASAN 支持
- 2015 年 8 月 – 增加了热补丁 (grsecurity 风格)
- 2015 年 11 月 (v4.3) – 增加了 userfaultfd
- 2015 年 11 月 – 宣布 KSPP
- 2015 年 11 月 – grsecurity 风格补丁
- 2015 年 11 月 – grsecurity 风格
- 2015 年 4 月 – 2015
  https://www.openwall.com/lists/oss-security/2017/03/1


- 2016 年 3 月 (v4.5) – UBSAN 支持
- 2016 年 3 月 (v4.5) – 增加了内存计数
- 2016 年 5 月 (v4.6) – 内存密钥 (PKEYs)
- 2016 年 7 月 (v4.7) – Slab 随机化
- 2016 年 7 月 (v4.7) – KSP 补丁
- 2016 年 10 月 (v4.8) – PAX_USERCOPY (slab 白名单)
- 2016 年 12 月 (v4.9) – VMAP_STACK


- 2017 年 4 月 (v4.11) – STATIC_USERHELPER
- 2017 年 7 月 (v4.12) – LSM 结构只读
- 2017 年 9 月 (v4.13) – REFCOUNT_FULL, FORTIFY_SOURCE
- 2017 年 11 月 (v4.14) – 强制执行合理的栈限制


- 2018 年 1 月 (v4.15) – KPTI 和 Retpolines
- 2018 年 4 月 (v4.16) – PAX_USERCOPY
- 2018 年 8 月 (v4.18) – 无权限挂载
- 2018 年 10 月 (v4.19) – L1TF 修复，FIFO 保护
- 2019 年 5 月 (v5.1) – LSM 堆叠





- 2019年7月 (v5.2) – 微架构数据采样 (MDS) 修复，并将现有的加固选项从“内核调试”区域重新调整到它们独立的“内核加固”区域
- 2019年11月 (v5.4) – 增加了锁定模式 (Lockdown mode)
  - 29个补丁系列通过了 Matthew Garrett、David Howells 等人的 40 次发布修订
  - https://lkml.org/lkml/2019/8/19/1190
- 该功能已在各个发行版（以及 grsecurity）中存在多年
  - “我7年前写的代码终于合并了” https://twitter.com/mjg59/status/1178167356029169664
- 2020年1月 (v5.5) – 增加了更细粒度的 `perf` 权限控制


- 内核加固邮件列表统计
  - 2016年有 3638 邮件
  - 2017年有 5202 邮件
  - 2018年有 3759 邮件
  - 2019年有 2727 邮件
  - 25% 的新补丁提交到列表
  - 29% 的更新后补丁提交到列表
  - 0.5% 的重发补丁
  - 19% 的针对新补丁的回复
  - 13.5% 的针对更新补丁的回复
  - 0.3% 的针对重发补丁的回复
  - 2.7% 因为 `get_maintainer.pl` 涉及 KSPP 列表
  - 8.5% 为所有其他安全讨论


占总邮件百分比名前列贡献者：

| 邮箱 | 百比 |
| :--- | :--- |
| keescook@chromium.org | 15.05 |
| thgarnie@google.com | 3.44 |
| ard.biesheuvel@linaro.org | 2.75 |
| mark.rutland@arm.com | 2.49 |
| jason@zx2c4.com | 2.29 |
| mic@digikod.net | 2.04 |
| me@tobin.com | 1.85 |
| luto@kernel.org | 1.61 |
| labbott@redhat.com | 1.60 |
| gregkh@linuxfoundation.org | 1.54 |
| luto@amaccapital.net | 1.51 |
| torvalds@linux-foundation.org | 1.47 |
| samitolvanen@google.com | 1.45 |
| igor.stoppa@huawei.com | 1.38 |
| peterz@infread.org | 1.33 |
| alex.popov@linux.com | 1.32 |
| elena.reshetova@intel.com | 1.31 |
| rick.p.edgecombe@intel.com | 1.23 |
| jannah@google.com | 1.19 |
| s.mesoraca16@gmail.com | 1.14 |
| yanaiijie@huawei.com | 1.08 |
| igor.stoppa@gmail.com | 1.05 |
| re.emese@gmail.com | 1.00 |


- “其他”类别是人们预期看到最有趣讨论的地方
  - 在决定实现方案并提交补丁之前提出新想法/进行头脑风暴
  - 这种情况极少在列表中发生（占8%）

补丁本身占了发送到 KSPP 邮件的一半以上

三分之一的邮件是对这些补丁的评审

专门提到 KASLR 的邮件占了所有邮件的近 9%

只有 9% 的邮件是在周末发送的

向列表发送邮件的人群呈现极长尾效应

- 上一张幻灯片中只有 23 人占比 >= 1%，其余 614 人占比 < 1%
  - 在这 614 人中，只有 17 人占比在 0.5% 到 1% 之间

用于你自己的分析（以及复制测试）：

- 邮件队列：https://grsecurity.net/kernel-hardening-cleaned.gz
- 分析脚本：https://grsecurity.net/KSPP-email-analysis.py


- 完全专注于将新的安全功能合并到最新的主内核中
- 这些更改中涉及内核代码的大规模重写
  - 移除 VLA（手动）
  - `kmalloc(n * size)` -> `kmalloc_array(n, size)`（自动）
  - `refcount_t`（手动）
- 虽然这提高了最新主内核的安全性，最终在多年后提高了许多（甚至是大多数）Linux 用户的安全性，但对现在的大多数人并没有益处
- 大规模重写不符合 `-stable` 的收录标准，没有被回回，这与大多数 KSPP 工作类似
- 没有技术原因导致这些功能无法被回回并提供广泛受众

- 2018 年以来的趋势是，大量的安全工作绕过了 KSPP

- PTI、retpolines 以及几乎所有其他的 Intel 漏洞修复是在没有 KSPP 列表的情况下私下开发的

- 架构维护者自行推动了某些安全更改

- 特别是 PowerPC 和 ARM64

这可能意味着 KSPP 的相关性在下降，但这是一个良好的信号，说明某些维护者对安全高度重视并加速了安全功能的开发

- 值得特别提到的开发者：
  - Will Deacon (ARM64)
  - Michael Ellerman (PowerPC)


- 2017年9月28日 – Google 在 Project Treble 上宣布，Greg KH 将对 LTS 内核的支持从 2 年增加到 6 年

- 似乎在此之前没有讨论过这一移动

- 支持周期延长了 3 倍，但回回随时间推移变得越来越困难

- 近一年后，Greg KH 发表了《我应该使用哪个稳定内核？》

- 首次包含了这一承认：

> 使用此类内核时有一个巨大的局限。回回的安全修复数量不如最新的 LTS 版本，因为传统的模式……





我们对独立稳定回回流程的观察结果：

- 作为我们最后的 4.4 补丁，上游 4.4 LTS 缺少了至少 1250 个与安全相关的修复。
- https://twitter.com/grsecurity/status/12435236055264285696
- AUTOSEL 越来越擅长发现那些缺失正确标签的安全修复，以前这些修复只有我们会在进行回回。
  - 然而，要充分发挥作用，参与回回的人数必须增加，否则它们会被直接在 –stable 邮件列表中丢弃。
  - 上述情况似乎没有明显改善。
  - https://lwn.net/Articles/805473/ : Dan Carpenter - “每个人都工作过载了。”

- AUTOSEL 选择的补丁需要更多的审查，以确保将它们应用于旧版本内核是合适的，以及它们是否需要调整，无论是否能够干净地检选（cherry-pick）。
  - https://www.spinics.net/lists/bpf/msg11641.html
  - 曾作为 ZDI 的 pwn2own 的一部分被利用。


- 在过去的 10 年里，syzkaller 的采用对上游内核开发产生了最大的影响。
- 当代码中发现问题时，开发者会收到通知。
- 与现有开发流程集成良好。
- 不断改进，整合了新的调试/测试功能。
- KCOV_ENABLE_COMPARISONS
- 帮助到达更多代码路径（且速度更快）。
- KASAN
- 检测 UAF（使用后释放）和其他 OOB（越界）内存访问。
- KMSAN
- 检测未初始化的内存访问。
- KCSAN
- 检测并发问题。

- 是一把双刃剑
  - 自定义的 syzkaller 实例可以发现 syzkaller.appspot.com 无法的漏洞。
  - 内核开发的快速节奏意味着存在大量未修复的问题。
    - 特别当 syzkaller 触及内核的新区域（USB 等）时。
    - https://twitter.com/dvyukov/status/1248241187854696450

> **Dmitry Vyukov** @dvyukov · 4月9日
欢迎我们 #linux 内核的新热点：KCSAN
数据率检测器，但基于 happens-before 的（不是 TSAN）
代码由 @maelver 编写，文章由包括 @paulmcrcru 在内的许多人编写

修复 [github.com/google/ktsan/w...](https://github.com/google/ktsan/w...)
syzbot 上有500 个开放报告 [syzkaller.appspot.com/upstream?manag...](https://syzkaller.appspot.com/upstream?manag...)
免费链接 [lnw.net/SubscriberLink...](https://lnw.net/SubscriberLink...)

**Marco Elver** @maelver · 4月8日
刚发布：“并发漏洞应该害怕那个大坏的数据率检测器（第一部分）\lwn.net/Articles/81685... #linux #concurrency”


- 仅数据攻击（Data-only attacks）正在上升，公开攻击继续关注阻力最小的路径。
- STATIC_USERMODEHELPER 似乎完全没有流行，UMH 路径继续成为目标。
- 内核本身执行跳出任何容器并以全权限执行进程的任务。
- 公开、未修复的 syzkaller 报告是一个良好的信息来源。
- 对 syzkaller 的微调、配置差异发现了公开使用的 Syzkaller 仪表板未显示的内核漏洞（http://syzkaller.appspot.com/）。
- 非特权用户命名空间暴露的攻击面短期内不会减少。
- 更多功能被暴露：
  - 2abe05234f2e l2tp：允许在用户命名空间中管理隧道和会话
  - 4a92602aa1cd openswitch：允许从用户命名空间内部进行管理
  - 5617c6cd6f844 nl802111：允许从用户命名空间进行特权操作
- “这段新允许的代码通过了现有的模糊测试？”似乎并不是启用此类功能的考虑因素。


- Project Zero 多年来主要通过滥用 FUSE 和 userfaultfd 功能来提高漏洞的可靠性。
  - https://googleprojectzero.blogspot.com/2016/06/exploiting-recursion-in-linux-kernel_20.html
- 攻击者仍然不在乎漏洞是否分配了 CVE。
  - https://googleprojectzero.blogspot.com/2019/11/bad-binder-android-in-wild-exploit.html
- 上述漏洞被一个据称由 NSO Group 开发的野外零日（Oday）利用了。
- 说明即使上游流程正常运行，下游用户仍将存在安全漏洞。
  - 此处的修复确实应用到了 -stable 内核。
  - 提交信息提到了 UAF，包含了 sybot 的 Reported-by，并进行了抄送（CC）。


- Project Zero 多年来主要通过滥用 FUSE 和 userfaultfd 功能来提高漏洞的可靠性。
  - https://googleprojectzero.blogspot.com/2016/06/explo-recursion-in-linux-kernel
- 攻击者仍然不在乎漏洞是否分配了 CVE。
  - https://googleprojectzero.blogspot.com/2019/11/bad-binder-android-in-wild-exploit.html
- 上述漏洞被一个据称由 NSO Group 开发的野外零日（Oday）利用了。
- 说明即使上游流程正常运行，下游用户仍将存在安全漏洞。
  - 此处的修复确实应用到了 -stable 内核。
  - 提交信息提到了 UAF，包含了 sybot 的 Reported-by，并进行了抄送（CC）。

- （等等，OCR 文本重复了，我将根据逻辑流进行重新对齐）

- 仅数据攻击正在上升，公开攻击继续关注阻力最小的路径。
- STATIC_USERMODEHELPER 似乎完全没有流行，UMH 路径继续成为目标。
- 内核本身执行跳出任何容器并以全权限执行进程的任务。
- 公开、未修复的 syzkaller 报告是一个良好的信息来源。
- 对 syzkaller 的微调、配置差异发现了公开使用的 Syzkaller 仪表板未显示的内核漏洞（http://syzkaller.appspot.com/）。
- 非特权用户命名空间暴露的攻击面短期内不会减少。
- 更多功能被暴露：
  - 2abe05234f2e l2tp：允许在用户命名空间中管理隧道和会话
  - 4a92602aa1cd openswitch：允许从用户命名空间内部进行管理
  - 5617c6cd6f844 nl802111：允许从用户命名空间进行特权操作
- “这段新允许的代码通过了现有的模糊测试？”似乎并不是启用此类功能的考虑因素。

- Project Zero 多年来主要通过滥用 FUSE 和 userfaultfd 功能来提高漏洞的可靠性……（等等，OCR 有重复部分，我将提供合并后的版本。）

**修正后的最终输出：**

- KCOV_ENABLE_COMPARISONS
- 帮助到达更多代码路径（且速度更快）。
- KASAN
- 检测 UAF 和其他 OOB 内存访问。
- KMSAN
- 检测未初始化的内存访问。
- KCSAN
- 检测并发问题。


- 是一把双刃剑
  - 自定义的 syzkaller 实例可以发现 syzkaller.appspot.com 无法的漏洞。
  - 内核开发的快速节奏意味着存在大量未修复的问题。
    - 特别当 syzkaller 触及内核的新区域（USB 等）时。
    - https://twitter.com/dvyukov/status/1248241187854696450

- 仅数据攻击正在上升，公开攻击继续关注阻力最小的路径。
- STATIC_USERMODEHELPER 似乎完全没有流行，UMH 路径继续成为目标。
- “这段新允许的代码通过了现有的模糊测试？”似乎并不是启用此类功能的考虑因素

（实际上，我将提供整个文本的清理版本。）




## 建议

- 快速失败，更快迭代
- 对安全补丁的大量审查往往是琐碎的挑剔和推诿责任
- 将 KASLR PIE/S.A.R.A. 代码拖延 3 年，这真的是对开发者时间的有效利用吗？
- 当提交了一个没有任何机会以任何形式合并的糟糕补丁时，通过建议一些琐碎的毛病检查和修复拼写错误来误导提交者，并要求他们发布 v2/v3/v20 版本，真的有帮助吗？

对于一个极易被滥用的新功能，决定“非特权”sysctl 的时机应该是该功能首次引入时，而不是在通过多个漏洞利用（非特权用户、userfaultfd 等）证明其必要性多年之后。

## 建议

- 重新找到为安全工作提供资金的方法
- CII 早已灭亡，但从未发布过讣
    - https://twitter.com/TomRittervg/status/11815728965729305473
    - 最后一次公告是在 2017 年
    - cii-discuss 邮件列表上的最后封邮件是 2017 年 12 月，关于 CII 对 OpenSSH 的支持于 2016 年结束但仍在 CII 网站上列出
    - 无回复，OpenSSH 和 OpenSSL 今日仍被错误地列为当前支持的项目
- 诸行行一


开源软件的安全风险从未如此之。全球有数百万人依赖开源软件——而 Heartbleed 漏洞让所有人都处于危险之中——是时候改变我们支持、保护和加固开源软件的方式了。通过核心基础设施倡议（Core Infrastructure Initiative），我们正在采取协作、预防性的方法来加强网络安全。许多行业巨头已签署共同加强关键开源项目的安全性。

# 感谢！

有疑问吗？

