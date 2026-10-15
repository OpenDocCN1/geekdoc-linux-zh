

## 前言

玩“shell”游戏很有趣。本书的写作目的就是让你的学习体验既有趣又有收获。自第一版出版以来，许多因我的书而受益的读者都联系过我，告诉我这本书让他们意识到 shell 编程根本不需要困难！通过示例学习使之变得简单有趣。事实上，正是因为这样的积极反馈，普伦蒂斯·霍尔出版社请我为 UNIX 和 Linux 用户、程序员和管理员制作了《UNIX® Shells by Example》的第四版。除了全书的更新内容外，它还包括三章全新的内容，全面涵盖了 GNU 工具，适合使用 Linux 的读者。随着 Linux 流行度的 meteoric 上升，似乎是把《Linux Shells by Example》的精华与《UNIX® Shells by Example》结合起来，制作一本涵盖 UNIX/Linux shell 世界各个方面的单卷本的好时机。

新章节包括第 2 章“Shell Programming QuickStart”，为希望快速了解 shell 编程结构及其差异的程序员提供入门介绍；第 15 章“Debugging Shell Scripts”，向你展示一个错误消息、其原因以及如何修复；以及第 16 章“The System Administrator and the Shell”，演示 shell 如何被系统管理员使用，从系统启动到关机。

撰写《UNIX® Shells by Example》是我 21 年教学和为 shell 程序员最常用的各种 shell 和 UNIX/Linux 实用程序开发课程的 culmination。我开发的课程笔记已被加州大学圣克鲁兹分校；加州大学戴维斯分校；Sun Microsystems；Apple Computer；Xilinx；National Semiconductor；LSI Logic；De Anza College；以及世界各地的众多厂商使用。根据客户的需求，我通常一次只教授一种 shell，而不是同时教授所有 shell。为了满足众多客户的需求，我为每种相应的 UNIX/Linux shell 和工具开发了单独的材料。

无论我教授的是“Grep, Sed, and Awk”、“Bourne Shell for the System Administrator”、“The Interactive Korn Shell”还是“Bash Programming”，总有一名学生会问：“我能得到一本涵盖所有 shell 以及 grep、sed 和 awk 等重要实用程序的书吗？awk 与 gawk 有何不同？如果我使用的是 Linux，这会起作用吗，还是仅适用于 Solaris？我应该买 awk 书，还是买 grep 和 sed 的书？有没有一本真正涵盖所有内容的书？我不想买三四本书才能成为 shell 程序员。”

作为回应，我可以推荐许多分别涵盖这些主题的优秀书籍，以及一些试图做到一切的 UNIX 和 Linux 书籍，但学生想要一本包含所有内容的书，而不仅仅是快速概览。他们想要工具、正则表达式、所有主要 shell、引用规则、shell 比较、练习等等，全部在一本书中。这就是这本书。

在撰写时，我思考了我的教学方式并以相同格式组织了章节。在 shell 编程课程中，第一个主题始终是对 shell 是什么以及它如何工作的介绍。然后我们讨论 grep、sed 和 awk 等实用程序——shell 程序员工具箱中最重要的工具。在学习 shell 时，它首先被介绍为一个交互式程序，在命令行上一切都可以完成，然后作为一种编程语言，其中编程结构在 shell 脚本中描述并演示。 （由于 C 和 TC shell 作为编程语言几乎相同，因此有单独的章节描述交互式使用，但只有一个章节讨论编程结构。）

编写脚本是一回事，但调试它又是另一回事。我使用 shell 已经很长时间了，以至于我几乎可以在程序发生之前就识别出 bug！但这些 bug 在你习惯错误消息及其含义之前很难找到。我增加了一章关于调试的内容，帮助你理解那些经常晦涩的错误消息的含义以及如何修复它们。由于 shell 的诊断信息可能不同，每个 shell 都列出了最常见的错误消息及其原因。

许多学生学习 shell 课程是为了迈向学习系统管理。我的教学同事 Susan Barr，她教授系统管理和 shell 编程，提供了她的丰富知识并撰写了一章来描述系统管理员如何使用 shell（第 16 章“The System Administrator and the Shell”）。

我一直发现简单的示例更容易快速理解，每个概念都以一个小示例捕获，然后是输出和对程序每一行的解释。这种方法已被证明非常受欢迎，那些从我的第一本书《Perl by Example》学习 Perl 编程，或从《JavaScript™ by Example》学习 JavaScript，以及从《UNIX® Shells by Example》学习编写 shell 程序的人都喜欢这种方法。

理解的另一个帮助是五种 shell 是并行讨论的。例如，如果你在一个 shell 中工作，但想了解重定向在另一个 shell 中是如何执行的，你会在其他 shell 章节中找到该主题的平行讨论。

在你只想获得足够的信息来提醒你某个特定命令是如何

