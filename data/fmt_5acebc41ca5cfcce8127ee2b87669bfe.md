
![](img/b418dfc0d37b54b9876d5e801170c507_215_0.png)

## 登录图形登录界面

在首次启动时，在通过 Red Hat Setup Agent 后，你会看到图形登录界面。在其他时候，你会先看到启动消息。其中一条消息显示 `Calibrating delay loop... xxx.xx`，`xxx` 是某个数字。BogoMIPS 是困扰新 Linux 用户的单词之一。

正如你可能所知，MIPS 是每秒百万指令的缩写——衡量计算机运行程序速度的指标。由于比较不同类型计算机的 MIPS 非常困难，MIPS 并不是一个非常好的性能标准。BogoMIPS 是“虚假的 MIPS”，指的是对计算机速度的一种指示。Linux 使用 BogoMIPS 来校准延迟循环，在循环中，计算机反复处理指令，直到过了指定的时间。

BogoMIPS 的数值范围从 1 到 3000 或更多，取决于处理器的类型（386、486 或 Pentium）。一个旧的 33MHz 80386DX 系统的 BogoMIPS 约为 6，而一个 66MHz 的 80486DX/62 系统显示的 BogoMIPS 约为 33。较新的 Pentium 系统的 BogoMIPS 高得多。例如，在一个旧的 200MHz Pentium MMX 系统上，Linux 报告的 BogoMIPS 为 398.13。然而，在带有 1.5GHz Celeron 处理器的笔记本电脑上，BogoMIPS 为 2,971.8。它比大多数最近的 3GHz 或更好的 Pentium 4 系统都要。

# 第二部分：探索红帽 Linux

如果你已经以 root 身份登录，可以使用 `shutdown` 命令来停止或重启系统。如果你已经使用其他用户名登录，可以通过输入以下命令来变为超级用户（你的输入将以**粗体**显示；我的注释将以*斜体*显示）：

```
su -
Password: (输入 root 密码并按回车)
```

当你通过输入 `su -` 变为 root 而不是只输入 `su` 时，你还会获得 root 的环境，包括 `PATH` 环境变量等设置。这使得你能够运行许多系统实用程序，而无需显式地指定它们的路径。

成为超级用户后，输入以下命令停止系统：

```
shutdown -h now
```
