

# 高级 Bash 脚本指南

## 38.3. 何处寻求帮助

作者不再对本文档提供支持或更新。他不会回答关于此书或通用脚本主题的问题。

> 如果你在学校作业方面需要帮助，请阅读本文以及任何任何其他参考书籍的相应章节。你最好的做法是利用自己的智慧和结果来解决问题。请不要浪费作者的时间。你既得不到帮助，也不会得到同情。[1399]

同样，请避免通过寻求请求、提供工作机会或“商业机会”来骚扰作者。他过得很好，既不需要帮助也不需要同情，谢谢。

请注意，作者将不会回答针对 Sun/Solaris/Oracle 或 Apple 系统的脚本问题。某些机构的阴暗高管和蜘蛛网般的公司律师一直将诉讼作为一种掠夺手段和/或针对开源社区的武器。因此，任何需要脚本帮助的 Solaris 或 Apple 用户请将他们的问题转给客户服务。

... 机制复杂但可能敏捷
在噪音极极抑制的状态下运行 ...

--CI-300 打印机手册

## 38.4. 制作本书使用的工具

### 38.4.1. 硬件

一台二手的 IBM Thinkpad 760XL 笔记本电脑（P166, 104MB RAM），运行 Red Hat 7.1/7.3。它运行很慢，键盘也很奇怪，但它比 2 号铅笔和 Big Chief 写字板好用得多。

升级到 770Z Thinkpad（P2-366, 192MB RAM），运行 FC3。有人想给一位饥饿的作家捐赠一台较型号的笔记本电脑吗 <?>

升级到运行 Mandriva 2011 的 T61 Thinkpad。不再饥饿了 <>，但并不自傲到不接受捐赠。

## 38.2. 软件与打印设备

- i. Bram Molenaar 强大的 SGML vim 文本编辑器。
- ii. OpenLaTeX，用于将 SGML 文档转换为其他格式的 DSSL 渲染引擎。
- iii. Norman Walsh 的 DSSL 样式表。
- iv. Norman Walsh 和 Leonard Mueller 编写《DocBook, The Definitive Guide》（O'Reilly, ISBN 1-56592-580-7）。这仍然是尝试编写 DocBook SGML 格式文档的人的标准参考书。

## 38.5. 致谢

社区的参与使得这个项目成为可能。作者优雅地承认，如果没有你们在各处提供的帮助和反馈，编写这本书是不可想象的。

Philippe Martin 将本文档的第一版本（0.1）翻译成了 DocBook/SGML。他目前在一家法国小公司担任软件开发人员，他喜欢致力于 GNU/Linux 文档和软件、阅读文学、弹音乐，并为了内心的平静与朋友聚会。你可能在法国或巴斯克地区某处遇到他，也可以通过 feloy@free.fr 联系他。

Philippe Martin 还指出，使用[括号]表示法可以传递位置参数 $9。（参见示例 4-5）。

Stephane Chazales 送了一份很长的修正、添加和示例列表。他不仅仅是一个贡献者，在一段时间内，他实际上承担了本文档共同编辑的角色。非常感谢！

Paulo Marcel Coelho Aragao 提供了许多主要和次小的修正，并贡献了许多有用建议。

我特别感谢 Patrick Callahan、Mike Novak 和 Paul Domokos，他们在本文档的初步版本（0.1）中发现了错误，指出了歧义，并建议了澄清和更改。他们对 shell 脚本和通用文档的生动讨论启发了我尝试让本文档更具读性。

我感谢 Jim Vanandt 指出了本文档 0.2 版本中的错误和遗漏。他还贡献了一个具有启发性的示例脚本。

非常感谢 Jordi Sanfeliu 允许使用他出色的树脚本（示例 A-16），并感谢 Rick Boivre 对其进行了修订。

同样，感谢 Michel Charpentier 允许使用他的 dc 因数分解脚本（示例 16-52）。

赞扬 Noah Friedman 允许使用他的字符串函数脚本（示例 A-18）。

Emmannel Rouat 对命令替换、别名和路径管理提出了修正和补充。他还贡献了一份非常好的 .bashrc 文件（附录 M）。

Steven 友善地允许使用他的进制转换脚本（示例 16-48）。他还做了许多修正和许多有用的建议。

Rick Boieve 贡献了极其精彩的递归 pb.sh 脚本（示例 36-11），修订了 tree.sh 脚本（示例 A-16），并对 monthlypm.sh 脚本（示例 16-47）提出了性能改进建议。

Florian Weiner 启发了我关于脚本测试的一个精点（参见示例 7-6）以及其他事项。

Oleg Pilon 提供了关于 cut 和 pidof 的建议。

Michael Zeke 扩展了空数组以演示一些惊讶的数组属性。他还贡献了 isspinner 脚本（示例 16-41 和示例 A-28）。

第 38 章 尾注

Marc-Jano Knoop 对 DOS 批文件提供了修正和澄清。

Hyun Jin Cha 在韩语翻译过程中发现了文档中的几种类型。感谢他指出这些问题。

Andreas Abraham 送了一个很长的打印错误列表和其他修正。特别感谢！

其他贡献脚本、提供有用建议和指出错误的人还有 Gabor Kiss、Leopold Toetsch、Jeff Tillier、Marcus Berg、 ...（后续文本省略） ... Eric Brandsberg, YongYe, Andreas Kühne, Pádraig Brady, Stephen Steinhauser（他也是四篇 HOWTO 的作者）。

感谢 Chet Ramey 和 Brian Fox 编写了 Bash，并从 kosh 中构建了优雅且强大的脚本功能。

非常感谢 Linux Documentation Project 的努力工作的志愿者们。LDP 拥有 Linux 知识和传说库，这使得本书得以出版。

感谢并赞赏 IBM、Red Hat、Google、自由软件基金以及所有为保持源代码自由而奋斗的优秀人士。

迟谢我的一年级老师 Miss Spencer，感谢她的鼓励、启发和情感支持，说服了我也许、也许并不是一个彻底失败的人。

感谢我的 Anita，她的启发和支持。

（这是 LDP 免责声明的变体）。不对本文档的内容承担任何责任。风险自使用这些概念和示例。文中可能存在错误、遗漏和不准确之处，可能会导致数据丢失、损坏系统或引发非自主触电，因此请采取谨慎措施。作者不

