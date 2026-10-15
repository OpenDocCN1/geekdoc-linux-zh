
# 如何在 Ubuntu 20.04 上安装 Matlab

> 原文：<https://blog.eldernode.com/install-matlab-on-ubuntu-20-04/>

MATLAB（MATrix LABoratory）是一种广泛使用的著名编程语言，它提供了一个数字计算环境。MATLAB 由 MathWorks 开发，提供矩阵操作、函数绘图和数据。在这篇文章中，你将学习如何在 Ubuntu 20.04 LTS 上安装 Matlab，以帮助你实现算法、创建用户界面并与用其他语言编写的程序进行交互。如果你拥有一台支持 VIP 的完美 Linux VPS，那么一切都会变得非常简单。选择你喜欢的 [Ubuntu VPS](https://eldernode.com/ubuntu-vps/) 包开始阅读本指南吧。

## 教程：在 Ubuntu 20.04 LTS 上安装 Matlab

为了让本教程更好地发挥作用，请考虑以下**先决条件**：

- 拥有 sudo 权限的非 root 用户。
- 要进行设置，请遵循我们在 Ubuntu 20.04 上的[初始服务器设置指南](https://blog.eldernode.com/initial-server-setup-on-ubuntu-20/)。

## 在 Ubuntu 20.04 上安装 Matlab

由于 MATLAB 应用程序是围绕 MATLAB 编程语言构建的，因此“命令窗口”在应用程序中主要用作交互式数学外壳，或用于执行包含 MATLAB 代码的文本文件。让我们通过本文的步骤，成为在 Ubuntu 20.04 上安装 MATLAB 的专家。

**第一步**：

一如既往，建议您通过[官方 Matlab 网站](https://www.mathworks.com/downloads/)下载最新的 MATLAB 安装包。选择 Linux 版本，并等待其下载完成。

![Download Matlab latest version](img/8c570c1a677a0db5208c91e3fe910aa8.png)

然后，您会在下载目录中找到**MATLAB 安装包**。

**第二步**：

显然，一旦您下载了安装包，就需要将其**解压**。请在您的下载目录中执行以下命令。此外，如果需要，您可以更新包的名称。

```bash
mkdir matlab
unzip -q matlab_R2019b_glnxa64.zip -d matlab
```

**第三步**：

在这一步中，安装将开始。请创建一个**安装目标目录**：`/usr/local/MATLAB/R2019b/`。然后，您应该通过导航到 **Matlab 目录**并运行以下命令来开始安装：

```bash
sudo mkdir -p /usr/local/MATLAB/R2019b/
```

**第四步**：

```bash
cd matlab
sudo ./install
```

如下所示，在这一步您应该**选择**您的首选安装方法。如果没有**文件安装密钥**，请选择**登录**方式。

![Installation Method](img/b15694f28f984601239b89e7df7682c1.png)

**第五步**：

接受**许可协议**的条款以通过这一步。

![Matlab License Agreement](img/19f6ad073d013da9e4feb8b093a1d4df.png)

**第六步**：

此时，系统会要求您创建一个 **MathWorks 帐户**或提供现有的**登录凭证**。

![create a MathWorks Account](img/fa02b4d4e29c4a4fc04efd839e93e9fe.png)

**第七步**：

现在，请选择您的 **MATLAB 许可证**。

![select your MATLAB License](img/acfe9e41229bd26014fd4687ca4c3537.png)

**第八步**：

同样，将`/usr/local/MATLAB/R2019b/`作为 MATLAB 安装的目标位置。

![choose installation folder](img/f9d9f5a018eebc0421185b1e2922a36c.png)

**第九步**：

是时候选择您需要安装的产品了。

![select the products to install](img/29c20d195150a0c0a96d5a9e44616174.png)

**第十步**：

现在，选择**创建到 Matlab 脚本的符号链接**。目标目录应保持默认的`/usr/local/bin`。

![Matlab scripts](img/a65d03bba366e910ffe7caf630cba3db.png)

**第十一步**：

如下图所示，您将看到 Matlab 安装**摘要**。

![Matlab installation summary](img/b386c9b8824931b8fa977e6e5042b39d.png)

**第十二步**：

至此，您可以看到 Matlab 的安装**进度**，请等待其完成。

![Matlab installation progress](img/fef867caffdbed636a3cf00f2599894a.png)

**第十三步**：

接下来，请激活您的 **Matlab 安装**，如下图所示。

![activate your Matlab installation](img/2bc4a042d9515de9f6263a681b74aac4.png)

**第十四步**：

激活产品时，单击“下一步”，然后继续。

**第十五步**：

当您按下“确认”按钮后，Matlab 安装将被激活。

![Activate Matlab installation](img/7cc2c399fe1f6d5c37ccaaca02d25280.png)

**第十六步**：

同样，一旦您按下**完成**按钮，Matlab 安装将正式结束。

![Activation is complete](img/55b886521c10f78adc153bffcd89b829.png)

**第十七步**：

现在，您可以考虑为 Matlab 应用程序**创建一个快捷启动器**。由于您仍在终端中，请运行以下 [Linux 命令](https://blog.eldernode.com/linux-commands-with-examples/)。您可以使用自己偏好的文本编辑器编辑`/usr/share/applications/matlab.desktop`，以确认 Matlab 所运行的版本。

**第十八步**：

现在，您可以在活动菜单中搜索关键词“Matlab”，并点击其图标来启动它。

**第十九步**：

当您看到下面的页面时，这意味着 **Matlab 正在启动**。

![Matlab is starting](img/bd8a24cbcf9851b59e251fed098495c0.png)

**第二十步**：

就是这样！您已经成功地在 Ubuntu 20.04 上**安装**了 Matlab。

![Final installation step](img/f318f6c5cf9c2fc3f83f73e06482c72c.png)

**第二十一步**：

```bash
sudo wget -qO /usr/share/icons/matlab.png http://bit.ly/2SUSFo3
sudo wget -qO /usr/share/applications/matlab.desktop http://bit.ly/2vcomAf
```

最后，请删除 Matlab 安装文件和临时目录：

```bash
rm ~/Downloads/matlab_R2019b_glnxa64.zip
rm -fr ~/Downloads/matlab
```

## 结论

在本文中，您已经学习了如何在 Ubuntu 20.04 LTS 上安装 Matlab。现在，请开始享受 MATLAB 的各项特性，并运行您的各种项目吧。
