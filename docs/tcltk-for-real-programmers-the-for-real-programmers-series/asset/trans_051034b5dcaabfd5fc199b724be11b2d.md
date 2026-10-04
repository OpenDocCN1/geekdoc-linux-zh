

此安装要求你将文件解压到临时目录，然后运行 `oratcl` 安装脚本 `install.tcl` 以将适当的文件复制到你的 Tcl 目录。

要安装 oratcl.DLLs：

- 1. 将“Tcl/Tk for Real Programmers”光盘放入光驱驱驱动器中。
- 2. 打开“运行”对话框。
- 3. 输入或浏览选择 `D:\extens\oratcl\oratcl125.exe` 作为要运行的文件。
- 4. 运行自解压 zip 文件。

![](img/fdcc2919568b5b6c9f5301d50a10e8d7_670_0.png)

- 5. 当初始窗口出现时，点击 OK 按钮。
- 6. 下一个窗口将让你有机会选择安装目录。

![](img/fdcc_2919568b5b6c9f5301d50a10e8d7_670_1.png)

你可以接受默认安装目录 (C:\ora_tmp) 或输入你偏好的目录路径。

- 7. 点击 Unzip 按钮。在安装扩展时，你会看到常规进度条。

## 附录 C 安装 Tcl/Tk 扩展

![](img/fdcc2919568b5b6c9f5301d50a10e8d7_671_0.png)

- 8. 安装完成后，点击 OK 按钮。
- 9. 点击 Close 按钮退出安装程序。

![](img/fdcc2919568b5b6c9f5301d50a10e8d7_671_1.png)

- 10. 切换到 C:\oratcl12.5\win 目录。
  cd C:\oratcl12.5\win

- 11. 运行 `install.tcl` 脚本，它将确定你正在运行的 Tcl 版本，并将适当版本的 oratcl DLL 复制到 Tcl 安装库目录下一个名为 oratcl25 的新目录中。

你可能需要将新目录添加到脚本的 `append_path` 变量中，以便使用 `package require Oratcl` 命令加载 oratcl。

## C.6.2 在 Unix 下安装 oratcl 扩展

oratcl 源代码以 gzipped tar 归包的形式提供。为了构建此包，你需要在系统中安装 Oracle C 库。

在 Unix 或 Linux 下构建 oratcl 的步骤如下：

- 1. 按照附录 B 中的描述构建并安装 Tcl/Tk。
- 2. 挂载“Tcl/Tk for Real Programmers”光盘。
- 3. 切换到 Tcl 和 Tk 分发版的父目录。
- 4. 解包 oratcl 分发包。

```
gunzip -c /cdrom/extens/oratcl/oratcl25.tgz | tar -xvf -
$ ls
oratcl-2.5 tcl18.0 tk8.0
```

此时，目录树应该类似于：

- 5. 切换到 oratcl-2.5 目录。
- 6. 运行 `configure` 脚本以创建一个新的 Makefile。
- 7. 编译包 (make)。

## C.7 plus

plus 补丁支持 Tcl 和 Tk 的 8.0 和 8.1 版本。

### C.7.1 在 MS-Windows 下安装 plus 扩展

dash、plus 和 img 补丁均已应用于 `plus` 目录下的自解压安装文件 `tk81plus.exe` 中的的 MS-Windows 可执行文件。

图像库和 img 库包含在 `tk81a2p1.exe` 文件中。该可执行文件是用 InstallShield 创建的，可以通过运行 `tk81a2p1.exe` 文件进行安装。

## 附录 C 安装 Tcl/Tk 扩展

运行此安装程序将在 bin 目录中创建 `wish81.exe` 和 `tsh81.exe` 的新副本，并将 `img1p3.dll` 的副本放置在 `lib\img1.dll` 目录中。

为了使用 img 扩展支持的新格式，你需要在脚本中使用命令 `load C:\program-1\tcl\lib\img1.dll\img118p3.dll`。

## C.7.2 在 Unix 下安装 plus 扩展

plus 补丁已应用于 /cdrom/extens/plus 目录下压缩的 tar 归包中的 Tcl 和 Tk 分发版。

你可以按照附录 B 中编译 Tcl 和 Tk 解释器的说明来生成新的解释器，但要从 /cdrom/extens/plus 提取分发版，而不是从 tcl_dist 分发版。

## C.8 sybtcl

“Tcl/Tk for Real Programmers”光盘提供的 sybtcl 扩展支持 Tcl 7.6 和 8.0 版本，以及 Tk 4.2 和 8.0 版本。为了使用此扩展，你还必须访问 Sybase SQL Server（版本 4.x、System 10 或 System 11），并备有 Sybase Open Client。

### C.8.1 在 MS-Windows 下安装 sybtcl 扩展

sybtcl DLL 文件存储在自解压 zip 文件 `extends sybtcl\sybtcl.exe` 中。为了使用 sybtcl，你还必须安装 Sybase DLL (libsydb.dll)。

此安装要求你将文件解压到临时目录，然后运行 `sybtcl` 安装脚本 `install.tel` 以将适当的文件复制到你的 Tcl 目录。

要安装 sybtcl.DLLs：

- 将“Tcl/Tk for Real Programmers”光盘放入光驱驱动器中。
- 打开“运行”对话框。
- 输入或浏览选择 `D:\extension\sybtcl\sybtcl125.exe` 作为要运行的文件。
- 运行自解压 zip 文件。
- 当初始窗口出现时，点击 OK 按钮。
- 下一个窗口将让你有机会选择安装目录。
- 点击 Unzip 按钮。在安装扩展时，你会看到常规进度条。
- 安装完成后，点击 OK 按钮。
- 点击 Close 按钮退出安装程序。
- 切换到 C:\oratcl12.5\win 目录。
- 运行 `install.tcl` 脚本，它将确定你正在运行的 Tcl 版本，并将适当版本的 oratcl DLL 复制到 Tcl 安装库目录下一个名为 oratcl25 的新目录中。
你可能需要将新目录添加到脚本的 `append_path` 变量中，以便使用 `package require Oratcl` 命令加载 oratcl。

## C.8.2 在 Unix 下安装 oratcl 扩展

oratcl 源代码以 gzipped tar 归包的形式提供。为了构建此包，你需要在系统中安装 Oracle C 库。

在 Unix 或 Linux 下构建 oratcl 的步骤如下：

- 1. 按照附录 B 中的描述构建并安装 Tcl/Tk。
- 2. 挂载“Tcl/Tk for Real Programmers”光盘。
- 3. 切换到 Tcl 和 Tk 分发版的父目录。
- 4. 解包 oratcl 分发包。

```
gunzip -c /cdrom/extens/oratcl/oratcl25.tgz | tar -xvf -
$ ls
oratcl-2.5 tcl18.0 tk8.0
```

此时，目录树应该类似于：

- 5. 切换到 oratcl-2.5 目录。
- 6. 运行 `configure` 脚本以创建一个新的 Makefile。
- 7. 编译包 (make)。

## 附录 C 安装 Tcl/Tk 扩展

![](img/fdcc2919568b5b6c9f5301d50a10e8d7_675_0.png)

## C.9 TclX

![](img/fdcc2919568b5b6c9f5301d50a10e8d7_676_0.png)

TclX 扩展支持 Tcl 和 Tk 的 8.0 和 8.1 版本。

### C.9.1 在 MS-Windows 下安装 TclX 扩展

TclX 扩展支持 Windows。Windows 版本的包含在光盘中。

要解压自解压 zip 文件：

- 1. 将“Tcl/Tk for Real Programmers”光盘放入光驱驱动器中。
- 2. 打开“运行”对话框。
- 3. 输入或浏览选择 `D:\extens\tclx\tcl800.exe` 作为要运行的文件。
- 4. 运行自解压 zip 文件。
- 5. 当初始窗口出现时，点击 OK 按钮。

![](img/fdcc_2919568b5b6c9f5301d50a10e8d7_676_1.png)

下一个窗口将让你有机会选择安装目录。
  你可以接受默认安装目录 (C:\tclx) 或输入你偏好的目录路径。

![](img/fdcc_2919568b5b6c9f5301d50a10e8d7_676_2.png)

- 点击 Unzip 按钮。在安装扩展时，你会看到常规进度条。

## 附录 C 安装 Tcl/Tk 扩展

- 8. 安装完成后，点击 OK 按钮。
- 9. 点击 Close 按钮退出安装程序。

![](img/fdcc2919568b5b6c9f5301d50a10e8d7_677_1.png)

