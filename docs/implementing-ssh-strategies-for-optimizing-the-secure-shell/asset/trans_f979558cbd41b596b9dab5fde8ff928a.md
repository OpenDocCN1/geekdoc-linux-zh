
现在，您的 Red Hat 8.0 机器上应该已启动了 SSH 服务器，端口为 22。要确认这一点，请输入 `netstat -an`，您应该看到与图 1.7 相同的结果。请注意，所有接口（以 `0.0.0.0` 表示）都在监听 22 端口，即 SSH 端口。

## OpenBSD 3.1

在 OpenBSD 3.1 服务器完成安装后，请使用您喜欢的 FTP 客户端（如命令行客户端或内置 Web 浏览器的 FTP 功能），从 `ftp://ftp.openbsd.org/pub/OpenBSD/OpenSSH/` 下载最新的压缩包。我将使用 3.5 版本（openssh-3.5.tgz）。将压缩包下载到您选择的目录；我推荐 `/usr/local/src`。文件下载完成后，请按照后续说明操作。

-   1. 从 shell 中，切换到 OpenSSH 包下载的目录：
    ```
    # cd /usr/local/src
    ```
-   2. 使用 `gunzip` 解压缩 tar 包：
    ```
    # gunzip -c openssh-3.5.tgz | tar xvf -
    ```
-   3. 切换到 `ssh` 目录：
    ```
    # cd ssh
    ```
-   4. 生成目标文件和依赖项：
    ```
    # make obj
    # make cleandir
    # make depend
    ```
-   5. 生成二进制文件：
    ```
    # make
    # make install
    ```

要启动守护进程，请切换到安装目录并启动服务：
```
# cd /usr/local/src/ssh
# ./sshd -p 22
```
注意，如果使用默认端口（22），则不需要 `-p` 选项。现在，您的 OpenBSD 3.1 机器上应该已启动了 SSH 服务器，端口为 22。要确认这一点，请输入 `netstat -an`，您应该看到与图 1.7 相同的结果。请注意，所有接口（以 `0.0.0.0` 表示）都在监听 22 端口，即 SSH 端口。

## Windows 2000 Server

在 Windows 2000 服务器完成安装后，请使用您喜欢的 FTP 客户端（如 ftp.exe 或 Internet Explorer），从 http://lexa.mckenna.edu/sshwindows/ 下载适用于 Windows 平台的最新 OpenSSH 版本。我将使用 3.5 版本（openssh35p1-3.zip）。将 zip 文件下载到您选择的目录；我推荐 c:\temp。文件下载完成后，请按照后续说明操作。

-   1. 双击 zip 文件并将两个文件提取到 c:\temp 目录。这两个文件应包含可执行文件（setupssh35.exe）和签名文件。
-   2. 将 setupssh35.exe 提取到 c:\temp 文件夹后，双击 setupssh35。
-   3. 应出现欢迎界面（见图 1.8）。选择“下一步”进入下一个界面。
-   4. 完整阅读许可协议（见图 1.9）。如果您同意，请选择“我同意”。如果您不同意，请点击“取消”，并将这本书送给硅谷资源匮乏的工程师们。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_47_0.png)

图 1.8 OpenSSH 向导的初始界面。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_48_0.png)

**图 1.9** OpenSSH 的许可协议。

-   5. 此时，您可以选择安装 SSH 的客户端和服务器部分，以及一些共享工具和菜单快捷方式（见图 1.10）。选择“下一步”。
-   6. 选择安装位置；我建议保留默认位置（见图 1.11）。选择“下一步”。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_48_1.png)

**图 1.10** OpenSSH 的组件选择界面。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_49_0.png)

**图 1.11** OpenSSH 的安装位置界面。

-   7. 选择快捷方式位置；我建议保留默认（见图 1.12）。点击“安装”开始安装程序。
-   8. 您应该看到安装正在进行中（见图 1.13）。
-   9. 在安装过程中，您应该看到一个文本框，提示您必须编辑密码文件（passwd）才能使 SSH 正常工作（见图 1.14）。这是安装完成后必须遵循的重要步骤。点击“确定”。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_49_1.png)

**图 1.12** OpenSSH 的开始菜单文件夹。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_50_0.png)

**图 1.13** OpenSSH 的安装界面。

-   10. 安装完成后，选择“完成”并保持“显示快速入门指南”勾选状态。
-   11. 快速入门指南现在应该会在记事本中出现。
-   12. 阅读指南中配置部分下的说明。
-   13. 从命令提示符，将目录更改为 OpenSSH 的 bin 目录。
    `c:\cd "Program Files\OpenSSH\bin"`
-   14. 要授予本地用户访问 SSH 守护进程的权限，请输入：
    `c:\Program Files\OpenSSH\bin\mkpasswd -l -u username >> ..\..\etc\passwd`

完成了！

切换到安装目录并启动服务：
`\Program Files\OpenSSH\bin\net start opensshd`

要确认服务已启动，请输入 `netstat -an`，您应该看到图 1.15 所示的屏幕。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_50_1.png)

**图 1.14** OpenSSH 适当安装的 passwd 文件编辑对话框。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_51_0.png)

**图 1.15** netstat -an 命令的结果。

请注意，所有接口（以 0.0.0.0 表示）都在监听 22 端口，即 SSH 端口。

## Commercial SSH

以下段落描述了使用商业版 SSH 的主要服务器。

### OpenBSD 3.1 和 Red Hat Linux 8.0

在 OpenBSD 3.1 或 Red Hat 8.0 服务器完成安装后，请使用您喜欢的 FTP 客户端（如命令行客户端或 Web 浏览器内置的 FTP 功能），从 ftp://ftp.ssh.com/pub/ssh/ 下载最新的压缩包。我使用的是非商业版 SSH，具体为 3.2.3 版本（ssh-3.2.3.tar.gz）。将压缩包下载到您选择的目录；我推荐 /usr/local/src。文件下载完成后，请按照后续说明操作。

-   1. 从 shell 中，切换到商业版 SSH 包下载的目录：
    ```
    # cd /usr/local/src
    ```
-   2. 使用 gunzip 解压缩 tar 包：
    ```
    # gunzip -c ssh-3.2.3.tar.gz | tar xvf -
    ```
-   3. 切换到 SSH 目录：
    ```
    # cd ssh-3.2.3
    ```
-   4. 编译源代码：
    ```
    # ./configure
    # make
    ```
-   5. 运行安装脚本：
    ```
    # make install
    ```

要启动守护进程，请切换到安装目录并启动服务：
```
# cd /usr/local/src
# ./sshd2 -p 22
```
注意，如果使用默认端口（22），则不需要 -p 选项。

要确认服务已启动，请输入 netstat -an，您应该看到与图 1.15 相同的结果。请注意，所有接口（以 0.0.0.0 表示）都在监听 22 端口，即 SSH 端口。

## Windows 2000

在 Windows 2000 服务器完成安装后，请使用您喜欢的 FTP 客户端（如 ftp.exe 或 Internet Explorer），从 www.ssh.com/support/downloads/secureshellserver/evaluation.mpl 下载适用于 Windows 平台的最新商业版 SSH（除非您已购买许可证，否则为评估版）。我使用的是 3.2.3 版本（SSHSecureShellServer-3.2.3.exe）。填写相应的评估表后，将可执行文件下载到您选择的目录；我推荐 c:\temp。文件下载完成后，请按照后续说明操作。

-   1. 双击该 .exe 文件。
-   2. 应出现欢迎界面（见图 1.16）。选择“下一步”进入下一个界面。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_52_0.png)

![](img/c99d6f526a5f9fa62f2c34daada85ad7_53_0.png)

图 1.17 商业版 SSH 的许可协议。

-   3. 完整阅读许可协议（见图 1.17）。如果您同意，请选择“是”。如果您不同意，请点击“取消”，并将这本书送给南达科他州布鲁金斯资源匮乏的工程师们。
-   4. 选择安装位置。我建议保留默认。（见图 1.18。）点击“下一步”。
-   5. 选择程序文件夹；我们建议保留默认（见图 1.19）。点击“下一步”。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_53_1.png)

图 1.18 商业版 SSH 安装的目标位置文件夹。

