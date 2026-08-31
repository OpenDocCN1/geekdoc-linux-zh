
# 如何在 Ubuntu 22.04 上安装 Yarn

> 原文：<https://blog.eldernode.com/install-yarn-on-ubuntu-22-04/>

![How to Install Yarn on Ubuntu 22.04](img/b2d1e81d62619ec13d46d7d9c9559993.png)

软件包管理器是一个安装、更新和管理您所需软件包的工具。借助此类工具，您可以随时获得软件所需的最新版本库，而无需自行搜索和检查这些库及其外部依赖，只需专注于开发软件核心。Yarn 也是一个包管理器，本文将教您如何在 Ubuntu 22.04 上安装 Yarn。此外，如果您想购买 [Linux VPS](https://eldernode.com/linux-vps/) 主机，可以访问 [Eldernode](https://eldernode.com/) 中的软件包。

## 什么是 Yarn？

Yarn（Yet Another Resource Negotiator）是 Node.js 的包管理器，用于在 JavaScript 中替代 NPM。它由该公司和开发者共同开发，旨在改进并解决 NPM 存在的问题。Yarn 由 Facebook、Google、Exponent 和 Tilde 开发。Yarn 允许用户使用自己的代码，并与世界各地的其他开发者共享。此外，它允许您使用其他开发者的解决方案来解决各种问题，从而使软件开发变得更加容易。

### Yarn 特性

- 从系统本地缓存安装软件包，无需互联网
- 并行安装软件包
- 严格绑定包版本
- 安装软件包速度快
- 在 CLI 中提供简单易读的命令
- 在包管理领域提供更多功能
- 支持多种插件

## 如何在 Ubuntu 22.04 上安装 Yarn

在安装 Yarn 之前，您需要在 Ubuntu 22.04 系统上安装 `npm`（节点包管理器）。`npm` 随 Node.js 一起提供。

可以借助 NodeSource 存储库来安装 Node.js。首先打开终端，为所需的 Node.js 版本设置 NodeSource 存储库。

要设置 NodeSource 存储库 16.x（LTS 版本），请执行以下命令：

```
wget -qO- https://deb.nodesource.com/setup_16.x | sudo -E bash
```

要设置 NodeSource 存储库 18.x（当前版本），请执行以下命令：

```
wget -qO- https://deb.nodesource.com/setup_18.x | sudo -E bash
```

现在，通过运行以下命令安装 Node.js 和 `npm`：

```
sudo apt install -y nodejs
```

您可以使用以下命令检查 Node.js 版本：

```
node --version
```

此外，您可以通过输入以下命令来检查 `npm` 版本：

```
npm --version
```

现在开始安装 Yarn。为此，请运行以下命令：

```
sudo npm install --global yarn
```

然后输入密码。

您可以使用以下命令检查 Yarn 版本：

```
yarn --version
```

在此步骤中，借助以下命令进入您现有的项目目录：

```
cd your_project
```

现在，您需要通过输入以下命令为您的项目安装最新的 Yarn 二进制文件：

```
yarn set version berry
```

然后使用以下命令再次检查 Yarn 版本：

```
yarn --version
```

收到的输出表明您的项目拥有最新版本的 Yarn。

## 如何在 Ubuntu 22.04 上使用 Yarn

以下命令可帮助您了解现有命令的用法：

```
yarn help
```

您可以借助以下命令创建一个目录：

```
mkdir my_project && cd my_project
```

要创建新项目，只需运行以下命令：

```
yarn init
```

输入上述命令后，系统会询问一系列与您的项目相关的问题，您可以通过按 `Enter` 使用默认值。上述命令还会生成 `package.json` 和 `yarn.lock` 文件，前者包含您提供的项目信息，后者包含关于项目依赖项的所有信息。

若要向项目中添加依赖项，可以运行以下命令之一：

```
yarn add (package-name)
```

```
yarn add (package-name)@(version)
```

```
yarn add (package-name)@(tag)
```

上述命令会下载并安装依赖包，并更新 `package.json` 和 `yarn.lock` 中的依赖详细信息。

您可以使用以下命令安装项目的所有依赖项：

```
yarn
```

或

```
yarn install
```

要升级项目的依赖项，请输入以下带有包名的命令之一：

```
yarn upgrade (package-name)
```

```
yarn upgrade (package-name)@(version)
```

```
yarn upgrade (package-name)@(tag)
```

若要删除项目中不再需要的依赖项，请运行以下命令：

```
yarn remove (package-name)
```

您可以使用以下命令更新 Yarn：

```
yarn set version latest
```

## 结论

本文教您如何在 Ubuntu 22.04 上安装和使用 Yarn。通过安装 Yarn，您可以安装软件包、启动新项目，并安全可靠地共享软件包。希望本文对您有所帮助，您可以轻松地在 Ubuntu 系统上安装 Yarn。
