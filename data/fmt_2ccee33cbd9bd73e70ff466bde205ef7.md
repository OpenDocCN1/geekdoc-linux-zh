
# 第三部分 ♦ 选择和安装 Linux 发行版

Red Hat Enterprise Linux 3 中的软件与 Fedora Core 1 中的软件包几乎完全一致。预计当 Red Hat 完成 Red Hat Enterprise Linux 4 时，Fedora Core 3 也是如此。至于将 Fedora 社区纳入 Fedora 开发中，Red Hat 在主页上表示：

> Red Hat 将保留对 Fedora Core 的编辑控制权——但将明确将外部开发者纳入技术决策过程，以确保与我们的目标一致。这是一次演进性的而非革命性的变化；自 Red Hat Linux 诞生以来，通过依赖和贡献开源软件，Red Hat 一直与外部开发者共享软件控制权。现在，Red Hat 将我们的新项目：Fedora 项目中更明确地与外部开发者共享打包控制权。

尽管在写本文时还没有正式的程序，但 Red Hat 表示，它预计根据人们对社区的贡献程度，让 Red Hat 之外的人员在 Fedora 规划和开发过程中承担重要角色：

欲了解更多关于 Fedora 项目目标的信息，请访问 `http://fedora.redhat.com/about/objectives.html`。

# 听取 Red Hat 社区的意见

正如你可能猜到的那样，追随 Red Hat 列车的社区成员对 Fedora/RHEL 的分裂产生了一些担忧。社区一些最大的担忧总结为以下问题：

- **Fedora 是一个真正的 Linux 发行版吗？** Fedora 被设定为一个项目，旨在筛选出进入 Red Hat 商业产品的软件。Red Hat 费很大确保知道知道 Red Hat 并不或支持支持 Fedora。 Fedora Fedora Fedora Fedora 所需的组件已经足够可以放入 RHEL 时，为什么 Red Hat 还要在乎 Fedora 是否是一个完全集成的发行版？
- **谁控制 Fedora？** 目前，在 Fedora 的功能、进度安排等其他关键部分方面，由 Red Hat 掌握着主导权。尽管 Red Hat 声称它将允许社区更多参与项目的关键部分，但到目前为止还没有这样做。社区为什么要支持一个他们没有控制权的 Linux 系统呢？

有趣的是，尽管过渡过程中存在令人困惑和沮丧的方面，开源社区的许多人仍然支持 Fedora 的工作。我认为这确实反映了 Red Hat 对开源的贡献是多么受推崇。这家公司在追求自身议程的同时，仍然被（某种程度上）信任为源码社区提供一些真正的价值。

# 第8章 运行 Fedora Core 和 Red Hat Enterprise Linux

尽管如此，我将用一个极佳且（我认为）是真实的反映来结束本节，反映了过渡到 Fedora 在源码社区看来是什么样的。以下是 fedora-devel 邮件列表的一封帖子，包含了 Konstantin Sergey 写的关于源码社区、Fedora 和 Red Hat Inc. 之间的虚构 IRC 会话（完整帖子请点击此处：`http://lwn.net/Articles/8360`）。让我用大家都能理解的格式转述一下目前的情况……

```
<rh_pr> 我们正在宣布 Red Hat 项目！一个基于社区的发行版！

<oss_crowd> rh_pr: 酷的。

<dev> rh_pr: 嗯... 我还没准备好。rh pr 正在推广 rhel

<oss_crowd> dev: 我们能做什么？

<dev> crowd: 我不确定。

<legal> dev: 在我可以之前什么都不要做。

<oss_crowd> 我们能做什么来帮助 Red Hat 项目？

<dev> crowd: uh... 文件和帮助类事务。

<oss_crowd> dev: 我们以前不都是做这些的？

<sales> 嘿，大家好。如果真的想要一个稳定的系统，不要用 fedora 项目它会吃掉你的大脑。改用 RHEL 吧。

<dev> sales: 闭嘴 销售部被取消了发言

<fedora_us> 嘿，看看我们为 red hat 设计的酷的社区驱动系统

<oss_crowd> fedora_us: 噢！

<rh_pr> 我们正在宣布 Red Hat 项目！一个基于社区的发行版！

<oss_crowd> rh_pr: 噢！ :我可以。

<legal> dev: 在我可以之前什么都不要做。

<oss_crowd> 我们能做什么来帮助 Red Hat 项目？

<dev> crowd: uh... 文件和帮助类事务。

<oss_crowd> dev: 我们以前不都是做这些的？

<salessales> 嘿，大家好。如果真的想要一个稳定的系统，不要用 fedora 项目它会吃掉你的大脑。改用 RHEL 吧。

<dev> sales: 闭嘴 销售部被取消了发言

<fedora_us> 嘿，看看我们为 red hat 设计的酷的社区驱动系统

<oss_crowd> fedora_us: 噢！

<rh_pr> 我们正在宣布 Red Hat 项目！一个基于社区的发行版！

<oss_crowd> rh_pr: 酷的。 :我可以。

<legal> dev: 在我可以之前什么都不要做。

<oss_crowd> 我们能做什么来帮助 Red Hat 项目？

<dev> crowd: uh... 文件和帮助类事务。

<oss_crowd> dev: 我们以前不都是做这些的？

<salessales> 嘿，大家好。如果真的想要一个稳定的系统，不要用 fedora 项目它会吃掉你的大脑。改用 RHEL 吧。

<dev> sales: 闭嘴 销售部被取消了发言

<fedora_us> 嘿，看看我们为 red hat 设计的酷的社区驱动系统

<oss_crowd> fedora_us: 噢！

<rh_pr> 我们正在宣布 Red Hat 项目！一个基于社区的发行版！

<oss_crowd> rh_pr: 酷的。 :我可以。

<legal> dev: 在我可以之前什么都不要做。

<oss_crowd> 我们能做什么来帮助 Red Hat 项目？

<dev> crowd: uh... 文件和帮助类事务。

<oss_crowd> dev: 我们以前不都是做这些的？

<salessales> 嘿，大家好。如果真的想要一个稳定的系统，不要用 fedora 项目它会吃掉你的大脑。改用 RHEL 吧。

<dev> sales: 闭嘴 销售部被取消了发言

<fedora_us> 嘿，看看我们为 red hat 设计的酷的社区驱动系统

<oss_crowd> fedora_us: 噢！

<rh_pr> 我们正在宣布 Red Hat 项目！一个基于社区的发行版！

<oss_crowd> rh_pr: 酷的。 :我可以。

<legal> dev: 在我可以之前什么都不要做。

<oss_crowd> 我们能做什么来帮助 Red Hat 项目？

<dev> crowd: uh... 文件和帮助类事务。

<oss_crowd> dev: 我们以前不都是做这些的？

<salessales> 嘿，大家好。如果真的想要一个稳定的系统，不要用 fedora 项目它会吃掉你的大脑。改用 RHEL 吧。

<dev> sales: 闭嘴 销售部被取消了发言

<fedora_us> 嘿，看看我们为 red hat 设计的酷的社区驱动系统
```
