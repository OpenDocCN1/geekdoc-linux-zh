

# Python

完全指南

Python 用户的必备手册

![](img/c72194f2c3aec198936695a665a5167c_0_0.png)

从今天起掌握 Python！

# 欢迎来到 Python
完全指南

Python 是一种多功能语言，它的流行日益并不令人意外。它与日常语言的相似性使其成为树莓派的完美伙伴，而树莓派通常是实际编程的第一步。但不要被它对初者的友好所迷惑——Python 有许多更高级的功能。在本杂志中，你将学习如何使用 Python 编程，发现奇的项目来提高理解，并寻找使用 Python 增强计算体验的方法。你还将创建有趣的项目，包括编写四旋无人机和从树莓派发送短信。让我们开始编码吧！

![](img/c72194f2c3aec198936695a665a5167c_2_0.png)

# Python

# 完全出版指南

Imagine Publishing Ltd
Richmond House
33 Richmond Hill
Bournemouth
Donet B1H 2EE
+44 (0)19202 56200
网站: www.imagine-publishing.co.uk
Twitter: @Imagine
Facebook: new.facebook.com/Imaginebookazines

出版总
Aaron Asadi

设计主管
Ross Andrews

制作编辑
Alex Hoskins

高级艺术编辑
Greg Whiteaker

设计师
Perry Ward-Wicks

摄影师
James Sheppard

印刷自
William Gibbons, 26 Planetary Road, Willenhall, West Midlands, WV1 3XT

在英国、美国及世界其他地区分销
Marketforce, 5 Churchill Place, Canary Wharf, London, E14 5HU
电话 0203 787 9060 www.marketforce.co.uk

在澳大利亚分销
Network Services (Bauer Media Group 分部门), 21 Civic Court, 66-68 Goubour Street,
Sydney, New South Wales Australia, Tel +61 2 8667 5288

> 免责声明
出版商对邮寄中的任何未经请求的材料或损坏不承担责任，这些材料的版权属于 Imagine Publishing Ltd。本杂志中的内容未经出版商书面许可，不得全部或部分复制。所有版权均已承认，并专门用于批评和评论目的。尽管本杂志已努力确保在印刷时所有信息都是正确的，但可用性可能会发生变化。本杂志完全独立，与此处提到的公司无任何附属关系。

Python 是 Python Inc. 的商标，已在美国及其他国家注册。
Python © 2016 Python Inc

Python 完全指南 第一版 ©2016 Imagine Publishing Ltd
ISBN 978 1785 462 689

![](img/c72194f2c3aec198936695a665a5167c_4_0.png)

# 目录

你可以在本杂志中找到的内容

![](img/c72194f2c3aec198936695a665a5167c_5_0.png)
![](img/c72194f2c3aec198936695a665a5167c_5_1.png)

用 Python 编码并创建！

![](img/c72194f2c3aec198936695a665a5167c_5_2.png)
![](img/c72194f2c3aec198936695a665a5167c_5_3.png)
![](img/c72194f2c3aec198936695a665a5167c_5_4.png)
![](img/c72194f2c3aec198936695a665a5167c_5_5.png)

# 从 Python 开始

8 大师课 发现 Python 基础

## 介绍 Python

## 使用 Python 创建

## 在树莓派上使用 Python

- **26 制作 Web 应用** 掌握这个入门项目
- **80 使用 Kivy 玩井字游戏** 编写一个简单游戏
- **86 制作 Pong 克隆游戏** 提升你的游戏技能
- **104 在树莓派上使用 Python** 优化你的代码
- **110 发送短信** 结合 Twilio 和树莓派
- **114 语音合成器** 使用 Espeak 库
- **116 编写四旋翼机** 使用树莓派制作无人机

- **32 为 Android 构建应用** 让你的应用移动随身携带
- **40 Python 技巧** 一系列实用技巧
- **88 编写太空侵入者克隆游戏** 玩 Pivaders 尽得乐趣
- **98 制作视觉小说** 开始一个故事
- **122 编写机器人** 使用 Twitter-API
- **124 控制 LED** 使用 GPIO

## 使用 Python 工作

- **50 替换 Shell** 使用-Bash
- **58 科学计算** 发现 NumPy
- **64 环境搭建** 使用-virtual
- **72 爬取数据** 使用 Beautiful Soup

![](img/c72194f2c3aec198936695a665a5167c_6_0.png)
![](img/c72194f2c3aec198936695a665a5167c_6_1.png)
![](img/c72194f2c3aec198936695a665a5167c_6_2.png)

# 欢迎来到 Python

Python 是一种多功能语言，它的流行日益并不令人意外。它与日常语言的相似性使其成为树莓派的完美伙伴，而树莓派通常是实际编程的第一步。但不要被它对初者的友好所迷惑——Python 有许多更高级的功能。在本杂志中，你将学习如何使用 Python 编程，发现奇的项目来提高理解，并寻找使用 Python 增强计算体验的方法。你还将创建有趣的项目，包括编写四旋无人机和从树莓派发送短信。让我们开始编码吧！

![](img/c72194f2c3aec198936695a665a5167c_2_0.png)

# Hello World

第一行以 shebang（符号 #!）开头，随后是 Python 解释器的路径。程序加载器使用此行来确定后续行是否需要解释。如果你在像 IDLE 这样的 IDE 中运行，不需要这样做。

解释器实际读取的代码只有一行。我们通过在调用函数后的括号中将 Hello World 传递给 print 函数。Hello World 没有加引号，以表示它是一个字面量，而不应被解释为源代码。正如我们预期的，Python 中的 print 函数会打印传递它的任何值。

你可以使用键组合 Ctrl+O 然后按 Enter 在 nano 中保存文件的更改。使用 Ctrl+X 退出 nano。

```python
#!/usr/bin/env python2
print("Hello World")
```

你可以通过在文件名前加 / 来运行 Hello World 程序——在这种情况下你输入：
hello_world.py

```
[Liam@liam-laptop Python]$ ./hello_world.py
Hello World
```

# 变量和数据类型

变量是源代码中的名称，它与内存区域关联，可以使用该区域存储数据，然后在代码中调用它。数据可以是许多类型之一，包括：

| 类型 | 描述 |
|---|---|
| 整数 | 存储整数 |
| 浮点数 | 存储小数 |
| 布尔 | 值为 True 或 False |
| 字符串 | 存储字符集合。"Hello World" 是一个字符串 |

![](img/c72194f2c3aec198936695a665a5167c_10_0.png)

> "变量与内存区域关联，可以使用该区域存储数据"

