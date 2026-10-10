
# 在 OS X、Linux 和 Windows 上入门 ASP.NET 5

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_0_0.png)
![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_0_1.png)
![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_0_2.png)
![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_0_3.png)
![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_0_4.png)

Agus Kurniawan

## 版权声明

在 OS X、Linux 和 Windows 上入门 ASP.NET 5

Agus Kurniawan

第一版，2015

版权所有 © 2015 Agus Kurniawan

## 目录

- 版权声明
- 前言
- 1. 准备开发环境
    - 1.1 ASP.NET 5
    - 1.2 系统要求
    - 1.3 开发工具
- 2. 在 OS X 上部署 ASP.NET 5
    - 2.1 入门
    - 2.2 部署 ASP.NET 5
    - 2.3 测试
        - 2.3.1 ASP.NET 控制台
        - 2.3.2 ASP.NET 5
        - 2.3.3 ASP.NET MVC
    - 2.4 开发工具
- 3. 在 Linux 上部署 ASP.NET 5
    - 3.1 入门
    - 3.2 部署 ASP.NET 5
        - 3.2.1 安装 Mono
        - 3.2.2 安装 libuv
        - 3.2.3 安装 DNVM
        - 3.2.4 安装 git
    - 3.3 测试
        - 3.3.1 ASP.NET 控制台
        - 3.3.2 ASP.NET 5
        - 3.3.3 ASP.NET MVC
    - 3.4 开发工具
- 4. 在 Windows 上部署 ASP.NET 5
    - 4.1 入门
    - 4.2 部署 ASP.NET 5
        - 4.2.1 安装 .NET
        - 4.2.2 安装 DNVM
        - 4.2.3 安装 git
    - 4.3 测试
        - 4.3.1 ASP.NET 控制台
        - 4.3.2 ASP.NET 5
        - 4.3.3 ASP.NET MVC
    - 4.4 开发工具
- 5. ASP.NET 5 开发
    - 5.1 入门
    - 5.2 构建 ASP.NET 5 控制台应用程序
        - 5.2.1 创建项目
        - 5.2.2 编写程序
        - 5.2.3 测试
    - 5.3 构建 ASP.NET 5 MVC 应用程序
        - 5.3.1 创建项目
        - 5.3.2 编写程序
            - 5.3.2.1 创建模型
            - 5.3.2.2 创建控制器
            - 5.3.2.3 创建视图
        - 5.3.3 测试
- 6. ASP.NET 5 RESTful 和 AngularJS
    - 6.1 入门
    - 6.2 创建项目
    - 6.3 编写程序
        - 6.3.1 创建模型
        - 6.3.2 虚拟数据库
        - 6.3.3 创建控制器
        - 6.3.4 创建视图
        - 6.3.5 AngularJS 程序
    - 6.4 测试
    - 6.5 下一步是什么？
- 源代码
- 联系方式

## 前言

本书旨在帮助任何希望开始使用 ASP.NET 5 core 的人。它描述了 ASP.NET 5 core 的部署以及 ASP.NET 5 core 的基本元素，并展示了如何使用几个 ASP.NET 5 core 功能。

Agus Kurniawan
柏林 & 德波克，2015 年 6 月

## 1. 准备开发环境

### 1.1 ASP.NET 5

ASP.NET 5 是一个轻量级且可组合的框架，用于构建 Web 和云应用程序。
ASP.NET 5 完全开源，可在 GitHub 上获取，http://github.com/aspnet/home。
撰写本书时，ASP.NET 5 目前处于预览阶段。

本书将重点介绍如何在 OS X、Linux 和 Windows 平台上开发 ASP.NET 5。我们使用 ASP.NET 5 core beta4。

### 1.2 系统要求

为了进行测试，我使用了 Debian/Ubuntu Linux、OS X Yosemite 和 Windows 8.1。你可以使用任何源自 Debian 的 Linux 发行版。

### 1.3 开发工具

一般来说，我们可以使用任何编辑器来编写 ASP.NET 5 程序。我建议使用 Sublime Text，[http://www.sublimetext.com/](http://www.sublimetext.com/)，来编写 ASP.NET 5 代码。微软还发布了 Visual Studio Code，你可以在 [https://code.visualstudio.com/](https://code.visualstudio.com/) 上下载。

## 2 在 OS X 上部署 ASP.NET 5

在本章中，我们将学习如何在 OS X 上部署 ASP.NET 5。

### 2.1 入门

在本节中，我们开始在 OS X 上部署 ASP.NET 5。在本书中，我使用 ASP.NET 5 预览版，beta4。请按照下一节的步骤进行安装。

### 2.2 部署 ASP.NET 5

要在 OS X 上安装 ASP.NET，你可以使用 brew，[http://brew.sh/](http://brew.sh/)。输入以下命令来安装 ASP.NET 5。

```bash
$ brew tap aspnet/dnx
$ brew update
$ brew install dnvm
```

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_12_0.png)

如果成功，你会看到一个你应该执行的任务。我们必须将 dnvm 添加到我们的配置文件中。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_13_0.png)

输入此命令。

```bash
$ nano ~/.bash_profile
```

然后，你会打开 nano 编辑器。你可以使用其他文本编辑器。将此脚本添加到 `~/.bash_profile` 中。

```bash
source dnvm.sh
```

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_14_0.png)

完成后，保存此文件。然后，关闭你的终端并重新打开，以便终端加载配置文件脚本。

下一步是升级。输入此命令。

```bash
$ dnvm upgrade
```

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_15_0.png)

现在你已经安装了 dnvm。它将用于管理 OS X 上的 ASP.NET 5 运行时。你可以通过输入此命令来验证 dnvm。

```bash
$ dnvm help
```

因此你会看到 dnvm 参数列表。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_16_0.png)

你还可以通过输入此命令来查看你的 DNX 运行时列表。

```bash
$ dnvm list
```

```text
dnvm alias <alias>
    display value of the specified alias

dnvm alias <alias> <semver>|<alias>|<package>
    <alias>
        <semver>|<alias>|<package>   the name of the alias to set
        the DNX version to set the alias to. Alternatively use the version of the specified alias

dnvm unalias <alias>
    remove the specified alias

dnvm [help|-h|--help|--help]
    displays this help text.

dnvm update-self
    updates dnvm itself.

agusk$ dnvm list

Active Version                Runtime Arch Location                 Alias
----- ------                  ---- ---- ----- ---                 -----
    *  1.0.0-beta4            mono            ~/.dnx/runtimes      default
agusk$
```

### 2.3 测试

为了测试我们的 ASP.NET 5，我们使用来自 [https://github.com/aspnet/Home](https://github.com/aspnet/Home) 的代码示例。我们克隆这些代码示例，然后使用 dnu 命令还原所有必需的库。输入这些命令。

```bash
$ git clone https://github.com/aspnet/Home
$ cd Home
$ dnu restore
```

如果你的 OS X 上没有 git，你可以通过 brew 安装它。

```bash
$ brew install git
```

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_18_0.png)

现在你准备好运行代码示例了。

#### 2.3.1 ASP.NET 控制台

要运行 ASP.NET 控制台，我们可以使用 dnx。首先，导航到 ConsoleApp 项目。输入这些命令。

```bash
$ cd samples/latest/ConsoleApp/
$ dnx . run .
```

如果成功，你可以在终端上看到消息 “Hello World”。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_19_0.png)

#### 2.3.2 ASP.NET 5

要运行 ASP.NET 5 应用程序，我们可以使用带有 kestrel 的 dnx。首先，导航到 HelloWeb 项目。
输入这些命令。

```bash
$ cd samples/latest/HelloWeb/
$ dnx . kestrel
```

现在打开浏览器，然后导航到 http://localhost:5004/。你应该会看到
ASP.NET 5 应用程序。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_20_0.png)

要停止 kestrel，你可以输入 `exit`。

```bash
exit
```

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_20_1.png)

#### 2.3.3 ASP.NET MVC

要运行 ASP.NET MVC，我们可以使用 dnx。首先，导航到 HelloMvc 项目。输入这些命令。

```bash
$ cd samples/latest/HelloMvc/
$ dnx . kestrel
```

现在打开浏览器，然后导航到 http://localhost:5004/。你应该会看到 ASP.NET MVC 应用程序。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_21_0.png)

要停止 kestrel，你可以输入 exit。

#### 2.4 开发工具

下一步是构建程序。要编写程序，你可以使用任何文本编辑器。微软还提供了 Visual Studio Code。它可以在 Windows、Linux 和 Mac 上运行。你可以在 [https://code.visualstudio.com/](https://code.visualstudio.com/) 上下载。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_23_0.png)

