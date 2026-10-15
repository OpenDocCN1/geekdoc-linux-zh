
融合仍然是一个关键问题。从理论上讲，通过蓝牙键盘和鼠标将安卓手机作为桌面，`Ubuntu` 可以切换到桌面模式。它的运行有点慢。`Ubuntu` 提供了高水平的控制，允许用户无缝地将文件从手机传输到智能电视，而 `Android` 则具有产生某种厂商锁定的潜力。

> 这点是没有意义的，因为目前 `GNOME` 还不支持融合，`Ubuntu Touch` 使用 `Mir` 和 `Wayland`，而 `GNOME` 已经让路。`Ubuntu` 团队试图通过在 `X11`、`Mir` 和 `Wayland` 之上堆叠来解决这个问题；毕竟，当连接时，桌面应用也应该能够在手机上运行。

## 另一个问题是 `Ubuntu Touch` 基于过时的 `Ubuntu 15.04`

另一个问题是 `Ubuntu Touch` 基于 `Ubuntu 15.04`——这是 `Canonical` 此后已停止推进的操作系统修订版。事实上，为了“激励”用户迁移，我们被关闭了软件库。`Canonical` 对 `Ubuntu 15.04` `Touch` 的工作已经结束。在许多软件包移除的终结之际，切换到更高版本已变得复杂。尽管如此，我们被告知所有展示的演示基准测试都是使用 `Ubuntu 15.04` 的预发布版本进行的——而且一个快速

`img/589a2610a2e4642c43669f03fe22f7ff_32_0.png`

## 焦点：多任务或缺乏多任务

上述 `Ubuntu Touch` 不支持真正的多任务

移动应用的核心哲学由 `PalmSource` 定义：认为由于与人体工程学相关的各种原因（参见 `Zen of Palm`，可用于 `https://designlearning.com/resources/zenofpalm/`），移动端不应该与桌面或笔记本应用太相似。

除了小组件，`Ubuntu Touch` 还有一些局限；类似于三星 `Android` 的早期版本，`Ubuntu Touch` 在没有多任务的情况下无法工作。一旦它被推到后台。这对应用程序来说是一个重大问题，因为它们无法在后台接收或显示消息。

与 `Android` 相关的问题是 `GPS`：如果你在导航时想打电话或写邮件，当你处于后台应用时，需要一个耗时的同步过程。`Ubuntu Touch` 团队认为这减少了功耗并增加了隐私性。在实践中，这对于智能手机手机用户来说可能是致命的。

演示手机末尾的“版本”检查确认了这一点。在没有方法对比的情况下，`Ubuntu Touch` 无法依赖 `Android` 理论上是不可用的不允许该 `PhoneGap` `Web` 切换将 `Ubuntu Touch` 相关的功能切换到桌面包后。

# 焦点聚焦

## 候选设备 `Fairphone`

我们获得了一台 `Fairphone2` 来评估其操作系统。这款荷兰环保手机可能价格昂贵，运行速度不是特别快，但它的优点是相对开放且符合伦理。事实上，在 `Canonical` 官方支持期间，该公司已经开始使用 `Ubuntu touch` 了。

暂且不考虑多任务问题，`p33` 的表现相当良好。`Classic touch` 作为屏幕创建运行正常，在我们（承认）很短的测试中没有出现任何问题。该产品还提供了一个网页风格的卡片，用于唤醒手机上休眠的应用。

在实际应用中，大多数功能都实现得非常完美；内存卡管理器在从上向下滑动时显示空白屏幕，这是一个在消费级操作系统中未见的广泛选项选择。它还带有命令行，开箱即支持点击。

遗憾的是，由 `JME` 开发者推广并引入 `Android` 的系统对 `Ubuntu touch` “过敏”——如果你是那种对权限提示过敏的人，这个操作系统绝对不适合你。

`img/589a2610a2e4642c43669f03fe22f7ff_34_0.png`

> 上方：`Ubuntu` 用户将看到显示器左侧熟悉的界面

`Android` 决定在 `BlackBerry BB10` 上实现基于滑动的导航。如果你找到一台 `Q10`，这需要在键盘旁边有大量的空白区域，而它缺少了大部分空间。在尝试从容使用该操作系统之前，需要一些练习。

然而，`Ubuntu touch` 在继承其传统方面方面很困难；状态栏仅在有请求时显示，正如你对 `iOS` 所预期的那样。`Ubuntu touch` 支持滑动——这一功能并未被废弃。

尽管如此，拥有开箱即用的全局功能对于 `BlackBerry Priv` 这种带有键盘的设备是有用的，这种体验正在发展中；考虑到浏览器（如 `Firefox`）的可用性或完全的 `Linux` 集成，并不是所有功能都能到位。

我们还获得了一台三星 `Galaxy S9` 来测试该项目，它运行起来非常烫，导致后台进程不断崩溃并重启。在错误的设备上，`Ubuntu touch` 并不是一个日常使用的平台。

> 上方：在 `Ubuntu` 上你无法逃避权限弹窗

在这个宇宙宇宙中，所有的 `bug` “也”都可以移动到移动空间。

`Ubuntu touch` 构建在自由硬件的基础上，从而确保它不会被 `OEM` 视为竞争，这似乎非常合逻辑。

然而，历史先例表明，这种方法与 `Symbian Foundation` 和 `Sourcebook` 一样，如果设备本身不推强大的硬件，操作系统将会走入歧途。

另一方面，`UbPorts` 与其基于社区的前身相比具有显著优势，这应该保持低成本。这意味着触控本身可能足够维持一段时间，直到某个厂商想要像 `Googlesoft` 那样对其边缘进行对冲。在这方面它是独一无二的。它只有一条进入介绍路线：通过 `Morris` 和 `Manfred Bortenschlager` 编写的《开发者指南》来了解更多关于公司的平台策略。

寻找硬件伙伴并不是唯一的问题。`UbPorts` 还需要找到一种方法让开发者能够为应用程序获得付款或捐赠——像 `Firefox OS` 这样的移动操作系统，缺乏变现能力很快变成了一个问题。

## 核心 `Linux`

## `Git`：带有某些 `Git` 强力工具的版本控制

学习一些令人兴奋且强大的内置工具，以加速并改进你的版本控制工作流

如果你目前一直都在使用 `Git`，你已经熟悉了 `Git` 命令，并知道如何对分支进行一些基本操作。问题在于，当你开始查看 `Git` 内置的高级强力工具时，`Git` 作为一个大型软件项目，拥有丰富的功能集合，可以涵盖各种场景。

`grep`，是 `grep` 系统的特殊版本，特别用于搜索 `Git` 仓库；而一个交互式工具允许你从任何地方提交更改。

在最后一期中，我们将对创建的 `Git` 仓库进行更改，运行命令 `git clone https://github.com/git/git` 来克隆此仓库并进入其中。我们假设仓库尚未被修改，或者如果你遵循了上一期的文章，你可能想在你的仓库副本中运行 `git reset --hard v2.18` 来移除已做的更改。

## 搜索 `Git` 项目

`Git` 有一个内置工具用于搜索 `Git` 源代码树。例如，在查看 `git` 中的代码时，注意 `git` 命令是由一个名为 `cmd_log` 的函数处理的，该函数执行了以下操作：

```
$ grep cmd_log
# _ output cut due to space
builtin/log.c:cmd_log(int argc, const
```

| `Git` | 编辑视图 帮助 |
|---|---|---|

| `run commit -c introduce text, new commit)` | | |

| `trace add object (print trace_line)` | | |

| `trace avoid unnecessary querying` | | | |

| `trace deindex` | | | |

| `submodule update submodule --from h to C` | | | |

| `submodule checkout-commit-a` | | | |

| `branch checkout --tag-name` | | | |

| `branch delete -d branch-name` | | | |

| `fetch -- clean up tags before rewriting` | | | |

| `fetch --prune --all` | | | |

| `merge branch -s/no-commit` | | | |

| `merge -s/no-ff` | | | |

| `merge --base adding short hashes` | | | |

| `merge --squash` | | | |

| `merge --pickix` | | | |

| `merge -s/no-ff` | | | |

| `merge-rebase --auto improve readability and of a sentence` | | | |

| `de-commit --auto improve readability and of syntax` | | | |

| `reset --hard [commit]` | | | |

| `reset --soft [commit]` | | | |

| `reset --mixed [commit]` | | | |

| `rm: Replace [commit] with it in` | | | |

| `tag -a --sign` | | | |
