
### 第 5 章：连接 Linux 工作站

#### 图 1. 查找共享目录和打印机列表

`img/6ee4859e736a0839007ea9afb576c195_158_0.png`

图 1 展示了当前共享目录和打印机的列表。每个项目都包含共享名称以及你在创建共享时指定的注释。图 2 显示了如何从`allaccess`计算机上的`Hetzen`共享进行此操作。

#### 图 2. 从 Windows 目录配置 Hetentzen 共享

`img/6ee4859e736a0839007ea9afb576c195_159_0.png`

#### 挂载目录

一旦你学会了从命令行界面挂载目录，就可以为每个用户设置登录文件。这些批处理文件将运行命令，在每个用户下次登录 Linux 时自动挂载目录。

只要你已经下载了本章开头介绍的`Samba`客户端包，就可以使用`smbmount`命令挂载共享网络目录。当然，你需要指定计算机名称、共享名称，通常还需要指定用户名和密码。

考虑第 4 章中的一个示例，当时你为一组飞机座椅生成器设置了共享目录。在你的 Linux 域服务器上，该共享目录位于`grateful`域中`nopaws`计算机的`/home/seatngr`。

这是一种使用`Red Hat`自定义的`GUI`可能会更快的情况。在`GUI`中，点击主菜单（`Main Menu`）|网络服务器（`Network Servers`）。这将打开`Nautilus`浏览器，查看与 Windows 网络上计算机的连接。如果你的 Linux 识别`NetBIOS`广播，它应该能够查看网络上的工作组（`Workgroups`）和域（`Domains`），如图 3 所示。

你可以通过在`Nautilus`浏览器的位置文本框中输入`smb:///`来查看 Windows 网络。这是一个统一资源标识符（`URI`），它可以定位网络上所有带有`Samba`服务器的 Windows 和 Linux 计算机。

自然，当你双击`GRATEFUL`图标时，你会看到`GRATEFUL`域内的服务器和工作站列表。你会看到所有配置为在该域共享文件和打印机的 Windows 和 Linux 计算机。在我的域中，我的`PDC`是`cosmicc`，我的 Linux 成员名为`nopaws`。

## Windows 网络管理员的 Linux 迁移

`img/6ee4859e736a0839007ea9afb576c195_160_0.png`

#### 图 3. 在 Linux GUI 中查看域

当我双击`nopaws`计算机时，系统会提示我输入用户名和密码，如图 4 所示。我可以在`PDC`或服务器成员上输入任何 Windows 用户名。你记得第 4 章提到的，Linux 计算机在`/etc/samba/smbusers`文件中存储了用户名数据库，该文件通过`smb.conf`文件中的以下命令激活：

```
username map = /etc/samba/smbusers
```

我输入了 Windows 用户名`waymonww`。在`PDC`上，我在`/etc/samba/smbusers`文件中将`waymonww`与 Linux 用户`waymon`关联。我可以使用第 3 章“设置你的服务器文件系统”中描述的`smbadduser`命令来实现此。如果`PDC`或服务器成员识别了你的用户名和密码，`Nautilus`然后将导航到共享目录。对于`nopaws`计算机，这包括在它的本地`smb.conf`配置文件中定义的共享目录。这些共享如图 5 所示。如你所见，这包括`smb.conf`文件末尾的共享，以及基本的主目录共享。在这种情况下，Linux 用户名是`waymon`，共享来自`/home/waymon`目录。

`img/6ee4859e736a0839007ea9afb576c195_160_1.png`

#### 图 4. 使用用户名和密码连接

`img/6ee4859e736a0839007ea9afb576c195_161_0.png`

#### 图 5. nopaws 计算机的共享目录

> 如果你以域用户身份连接，你将在`Nautilus`中看到其后的共享名称——即使该用户在目标服务器上没有主目录。

假设`PDC`或成员服务器验证了你的凭据，`Nautilus`将带你进入该域共享目录的图形视图。我将在**图 6**中说明其工作原理，它是`nopaws`计算机上`[seatengr]`共享文件的图形列表。

`img/6ee4859e736a0839007ea9afb576c195_161_1.png`

#### 图 6. 来自共享目录的文件

你现在可以通过图形化方式管理此目录下的文件。例如，你可以通过将文件拖到桌面上的垃圾桶图标来删除文件。你可以将文件复制到`Nautilus`窗口中打开的目录。`Nautilus`会识别扩展名，双击文件将在适当的应用程序（如`GNOME`文本编辑器）中打开它。

但作为管理员，你希望为你的用户设置适当的登录文件。首先，让我们测试一些你可以使用的命令。例如，如果我想挂载来自`nopaws` `[seateng]`共享的`/home/seateng`目录，我可以运行以下命令：

```
# mount -o username=waymonwn //nopaws/seateng /home/seateng

password:
```

此命令挂载了`[seateng]`共享的`/home/seateng`。我可以在`/home/seateng`运行以下命令，这可以让你看到`smb.conf`文件中的共享。对于`nopaws`计算机，这包括在其本地`smb.conf`配置文件中定义的共享。这些共享如图 5 所示。如你所见，这包括`smb.conf`文件末尾的共享，以及基本的主目录共享。在这种情况下，Linux 用户名是`waymon`，共享来自`/home/waymon`目录。

但作为管理员，你希望为你的用户设置适当的登录文件。首先，让我们测试一些你可以使用的命令。例如，如果我想挂载来自`nopaws` `[seateng]`共享的`/home/seateng`目录，我可以运行以下命令：

```
### mount -s /home/seateng
```

在 Linux 中，`umount`命令会卸载共享。挂载和卸载命令有一个缺点：它们只能以`root`用户身份执行。为了在 Windows 网络中，你可以以`root`用户身份执行以下步骤，以允许普通用户挂载和卸载目录：

1. 以`root`用户执行：

```
### chmod +s /bin/smbmnt
# chmod +s /bin/smbmount
```

2. 现在你已经看到`smbmnt`和`smbmount`命令对普通用户有效，你可以执行：

```
$ smbmount //nopaws/seateng /home/seateng -o username=waymon

password:

$ ls /home/seateng
```
