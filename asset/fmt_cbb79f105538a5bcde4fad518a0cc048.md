
虽然我们同时提供了 Ubuntu 10.04 的 32 位和 64 位版本，并且本书是为 10.04 版本编写的，但你可能决定尝试更新的 Ubuntu 版本。在这种情况下，只需前往 http://ubuntu.com 然后下载 CD 映像或请求寄送一份拷贝即可。不管你选择哪张 Ubuntu Server CD，使用它们都相对容易。只需将你想要安装的版本插入计算机并从 CD-ROM 启动。当 CD 启动时，你会在屏幕上看到一些选项，但要安装 Ubuntu Server，只需选择 `Install Ubuntu Server`。启动的安装程序会询问一些与大多数安装光盘类似的相当直接的问题，如果你遇到困难，只需翻到第 1 章，里面有安装过程的更深入讲解。

### Acknowledgments

JORGE，如果没有你，我不会参与这本书。我是因 Jorge 而使用 Ubuntu 的众多人中的一员。他的热情极具感染力，我数不清他有多少次向我介绍某个酷炫的新程序或工具，我起初嗤之以鼻，最终却不知不觉地开始使用。

Debra 和 Mako，能与你们二位一起在这个项目上工作非常棒，感谢你们提供的机会和指导。还要感谢 Matthew 在支持章节提供的帮助。Robert，非常感谢你出色的细节关注以及追查我所有打字错误和失误的地方。感谢 Bill “the Cloud” Childers 为 UEC 部分提供了设备。

特别感谢 Dustin、Nick、Jamie、Kees、Alan、Mathias、Thierry 以及 Ubuntu Server 团队的其余成员，在整个过程中给予了我们所有优秀的反馈和帮助。

——Kyle Rankin

### Introduction

本介绍概述了 Ubuntu 和 Ubuntu Server。在简短的欢迎之后，它包括了自由软件、开源以及 GNU/Linux 的简要历史，以及 Ubuntu 项目本身的历史，重点关注 Ubuntu 圈中的一些主要人物。本介绍结束于本书其余部分将继续的地方：Ubuntu Server 项目的历史，以及该项目目标和成就的概述。

### Welcome to Ubuntu Server

在成立刚过六年多的时间里，Ubuntu 已成为最受欢迎的基于 GNU/Linux 的操作系统之一。然而，在此过程中，公众的认知却不成比例地集中在 Ubuntu 作为桌面操作系统的角色上。虽然对于我们这些参与项目的人来说，所有的受欢迎都是受欢迎的，但这种成功有时掩盖了 Ubuntu 作为服务器操作系统的坚实基础。对于我们这些帮助构建 Ubuntu 服务器特定功能并每天使用它的人来说，这既不幸又不公平。自第一天起就被设计并用作服务器，Ubuntu 支持了一个服务器团队，该团队是 Ubuntu 社区中最早活跃的团队之一，也是最成功的团队之一。尽管认知在很大程度上已经改变，但许多潜在用户——甚至一些现有的 Ubuntu 用户——仍然常常认为 Ubuntu 是用于桌面的。

也许只是人们对 Ubuntu 在桌面上的易用性感到惊讶——尤其是在早期，桌面 GNU/Linux 发行版的期望值很低时——公众的关注自然就偏离了 Ubuntu 的服务器产品。很多其他 GNU/Linux 发行版在服务器上运行得很好，但扎实的桌面体验仍然让许多用户感到惊讶。因此，当人们谈论 Ubuntu 时，他们往往倾向于谈论桌面。另一方面，也许人们只是认为如此精致的桌面一定是以牺牲服务器导向的功能和支持为代价的。当然，并没有做出任何牺牲。

在很大程度上，时代已经改变。Ubuntu Server 团队继续不懈地工作，既改善 Ubuntu 服务器用户的体验，也帮助推广 Ubuntu 作为服务器解决方案。文档、推荐、服务器软件认证、来自各种来源的支持合同、培训课程等等，都促成了 Ubuntu 成为服务器领域的一股强大力量。尽管其桌面资质并未减弱，但 Ubuntu 的服务器实力也越来越难以忽视。在过去两年里，Ubuntu 开始在 GNU/Linux 服务器市场中成为主要参与者。

最重要的是，推荐不断传播，早期 Ubuntu Server 用户的小群体传播了这一消息。越来越多的人每天选择 Ubuntu 作为他们的服务器。事实上，这本书只是 Ubuntu 在服务器上发展到何种程度的最新有力例证。人们现在不仅知道 Ubuntu 可以在服务器上运行，而且知道它运行得很好。这本书能够出版，只是因为存在市场。这个市场由那些听说了 Ubuntu 在服务器上的好消息并准备自己一试的人组成。欢迎。我们希望能帮助让这一过程更轻松。我们已经走了很远，而我们才刚刚开始。

### Free Software, Open Source, and Linux

Ubuntu Server 的历史在很大程度上必须是 Ubuntu 本身的历史。Ubuntu 的历史在很大程度上必须是自由软件运动和 Linux 内核的历史。虽然成千上万的个人以某种形式为 Ubuntu 做出了贡献，但该项目之所以成功，只是因为成千上万更多的人间接为 Ubuntu 的成功奠定了技术、社会和经济基础。虽然在许多其他地方都可以找到有关自由软件、开源和 GNU/Linux 的介绍，但没有这些内容，任何对 Ubuntu 的介绍都是不完整的

out a brief discussion of these concepts and the people and history behind them. It is around these concepts and within these communities that Ubuntu was motivated and born. Ultimately, it is through these ideas that it is sustained.

### Free Software and GNU

In a series of events that have almost become legend through constant repetition, Richard M. Stallman created the concept of free software in 1983. Stallman grew up with computers in the 1960s and 1970s, when computer users purchased very large and extremely expensive mainframe computers, which were then shared among large numbers of programmers. Software was, for the most part, seen as an add-on to the hardware, and every user had the ability and the right to modify or rewrite the software on his or her computer and to freely share this software. As computers became cheaper and more numerous in the late 1970s, producers of software began to see value in the software itself. Producers of computers began to argue that their software was copyrightable and a form of intellectual property much like a music recording, a film, or a book’s text. They began to distribute their software under licenses and in forms that restricted its users’ abilities to use, redistribute, or modify the code. By the early 1980s, restrictive software licenses had become the norm.
