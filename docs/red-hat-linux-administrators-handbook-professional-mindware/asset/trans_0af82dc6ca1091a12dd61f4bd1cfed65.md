

## 配置匿名 FTP 上传

如果你需要一个允许匿名用户上传文件的传入或收件箱目录，请执行以下操作：

- 在 `/ftp` 目录下创建一个用于上传的子目录。该目录通常被称为“incoming”，因此这里使用该名称。
- 将以下行添加到你的 `/etc/ftpaccess` 文件中：`upload /home/ftp /incoming yes root ftp 0600 nodirs`
- 将 `/home/ftp/` 更改为适当的目录。例如，如果你的 `/ftp` 实际上是 `/data/ftp`，请将上述行中的 `/home/ftp/` 更改为 `/data/ftp`。此外，如果你希望允许匿名用户能够在 `/ftp/incoming` 下创建子目录，请移除上述行中的 `nodirs` 选项。
- 运行以下命令：
  ```bash
  chown -R root.ftp /ftp/incoming
  chmod -R 1733 /ftp/incoming
  ```
  `chown` 命令将 `root` 设置为 `incoming` 目录的所有者，并将 `ftp` 设置为该目录的组。`chmod` 命令更改 `incoming` 目录的权限，使得 `root` 具有读取、写入和执行（`rwx`）权限，而组和用户（everyone）具有写入和执行（`wx`）权限。它还设置了目录及其所有文件的粘滞位（sticky-bit），从而保护文件不被普通用户删除。通常，当一个目录对所有人设置了写入和执行权限时，该系统的任何用户都可以删除该目录中的文件。粘滞位通过仅允许文件的创建者删除文件来阻止这种行为。由于 FTP 服务器以 `root` 为所有者写入文件，因此除了 `root` 以外，没有人被允许删除上传的文件。
- 确保你的 `/etc/ftpaccess` 文件中至少在一个类定义中列出了匿名用户类型。默认情况下，`real`、`guest` 和 `anonymous` 都包含在默认的 `all` 类中，因此除非你更改了默认类定义，否则无需执行任何操作。

完成这些步骤后，以匿名用户身份 FTP 到服务器，并确保你只能将文件上传到指定目录。由于你没有对 `/ftp/incoming` 目录的读取访问权限，你不应该能够使用 `ls` 命令看到你上传的文件。但是，如果你提供正确的文件名，你仍然可以下载已上传的文件。

## 增强匿名 FTP 安全性

创建匿名 FTP 站点本身就是一种安全风险，而具有可上传目录会增加该风险。然而，许多组织多年来已成功运行匿名 FTP 服务器，因此不要过于沮丧——只要保持谨慎即可。以下是一些增强匿名 FTP 服务器安全性的准则：

- 确保 `/etc/passwd` 中的 `ftp` 账户使用的是无效密码。例如，你在 `passwd` 文件中的 `ftp` 账户条目应如下所示：
  ```text
  ftp::14:50:FTP User:/home/ftp:/bin/true
  ```
- `/ftp/bin` 目录的所有者应为 `root`，而不是 `ftp` 账户。你在 `/ftp/bin` 目录中的二进制文件，如 `ls`、`compress` 和 `tar`，也必须由 `root` 用户拥有。`/ftp/bin` 目录及其内容应仅具有可执行权限。运行以下命令以确保 `/ftp/bin` 目录中的所有文件都仅具有可执行权限：
  ```bash
  chown -R root.root /ftp/bin; chmod 111 /ftp/bin
  ```
- `/ftp/etc` 目录的所有者应为 `root` 用户，且必须仅具有可执行权限。你可以使用以下命令来实现：
  ```bash
  chown -R root.root /ftp/etc; chmod 111 /ftp/etc
  ```
- `/ftp/etc` 目录的内容必须是只读的，并且必须由 `root` 拥有。运行以下命令以确保权限设置正确：
  ```bash
  chown -R root.root /ftp/etc; cd /ftp/etc; chmod 444 *
  ```
- 切勿将你的 `/etc/passwd` 或 `/etc/group` 文件复制到 `/ftp/etc` 目录中。`/ftp/etc/passwd` 和 `/ftp/etc/group` 文件是满足那些在以 `/ftp` 为根目录运行时查找这些文件的程序的虚拟文件，这是由于服务器的 `chroot` 操作所致。
- 作为一般的安全规则，确保 `/ftp` 中没有任何文件或目录由 `ftp` 用户拥有。

## 创建来宾 FTP 账户

来宾 FTP 账户是一个具有真实用户名和密码的真实账户。当来宾用户登录到 FTP 服务器时，服务器会对来宾用户的家庭目录执行 `chroot` 操作，从而使来宾用户的家庭目录表现为整个文件系统。

设置来宾账户最简单的方法是使用 `anonftp` 软件包，即使你不想提供匿名 FTP 服务。只是为了创建单个来宾账户而暂时安装该软件包。以下是创建来宾账户所需的步骤：

1. **创建来宾用户账户。**
   成为 `root` 并以创建真实用户账户相同的方式创建来宾用户账户。此示例假设该来宾用户账户名为 **mrfrog**，并且是使用通常的 `useradd` 命令创建的，如下所示：
   ```bash
   useradd mrfrog
   ```
   使用以下命令为 `mrfrog` 设置所需密码：
   ```bash
   passwd mrfrog
   ```

2. **停止 Telnet 访问。**
   使用以下命令将 `mrfrog` 的默认 shell 更改为 `/bin/true`：
   ```bash
   chsh mrfrog
   ```
   当提示输入新 shell 路径时，输入 `/bin/true`。这禁止 `mrfrog` 通过 Telnet 访问系统，以确保 `mrfrog` 无法使用 Telnet 访问服务器并浏览其他用户或系统文件。编辑 `/etc/passwd` 文件，并在现有的家庭目录路径后追加 `./`。例如，如果 `/etc/passwd` 文件中有一行类似于以下内容：
   ```text
   mrfrog:1:516:519::/home/mrfrog:/bin/true
   ```
   请将其更改为：
   ```text
   mrfrog:1:516:519::/home/mrfrog./:/bin/true
   ```
   `./` 序列用于告知 FTP 服务器在 `/home/mrfrog` 目录上执行 `chroot` 操作。

   编辑 `/etc/shells` 文件，并在文件末尾添加 `/bin/true`。这使得 `/bin/true` 程序成为一个有效的 shell 选项。请注意，`/bin/true` 程序不做任何事情，并且在运行后立即退出。这使其成为需要验证但拒绝用户任何操作然后退出的 shell 的良好候选者。由于从 shell 退出会导致用户注销，因此当尝试进行 Telnet 连接时，用户永远没有机会做任何事情。

3. **安装 anonetftp 软件包。**
   如果你的系统上已经安装了 `anonftp` 软件包，请跳过此步骤并转到第 4 步。否则，获取最新的 `anonetftp` 软件包并通过运行 `rpm` 命令进行安装：
   ```bash
   rpm -ivh anonetftp-3-0-6.i386.rpm
   ```
   你的 `anonetftp` 软件包名称会根据你的系统架构和 `anonetftp` 版本而变化。此外，如果你没有 FTP 服务器，例如 `wu-ftp`，`anonetftp` 软件包将不会安装。

4. **将 anonetftp 软件包文件复制到来宾用户的家庭目录。**
   更改目录到 `/ftp` 并使用以下命令将所有文件和目录复制到 `/mrfrog`：
   ```bash
   tar cvf - * | ( cd /mrfrog ; tar xvf - )
   ```
   你真正需要的只有 `/ftp/bin`、`/ftp/etc` 和 `/ftp/lib` 目录。你可以删除 `/ftp/pub` 目录或你在 `/ftp` 目录中可能已有的任何其他目录。

5. **更新 `/mrfrog/etc/passwd` 和 `/mrfrog/etc/group` 文件。**
   编辑 `/mrfrog/etc/passwd` 文件并删除 FTP 用户的行。追加 `/etc/passwd` 文件中 `mrfrog` 的精确密码行。但是，删除 `mrfrog` 的密码并将其替换为 `*` 以使其无效。例如，该行：
   ```text
   mrfrog:1:516:519::/home/mrfrog./:/bin/true
   ```
   需要将此行复制到 `/mrfrog/etc/passwd`，并且需要替换密码，使得该行看起来像以下这样：
   ```text
   mrfrog*:516:519::/home/mrfrog./:/bin/true
   ```
   修改 `/mrfrog/etc/group` 文件并添加在 `/etc/group` 中找到的 `mrfrog` 行。这假设你没有以某种方式禁用 Red Hat 的默认功能，即自动创建与新用户同名的私有组。换句话说，当你使用 `useradd` 程序创建用户时，它会自动为该用户创建一个同名的私有组。因此，当你创建 `mrfrog` 时，你应该也自动在 `/etc/group` 中创建了一个名为 `mrfrog` 的组。如果你更改了 `useradd` 程序的默认行为或手动创建了用户，请为该用户创建一个组并将其添加到 `/mrfrog/etc/group` 文件中。此外，从 `/ftp/etc/group` 文件中删除 `ftp` 组。

6. **设置目录和文件权限。**
   更改目录/文件权限如下：
   ```bash
   chown mrfrog.mrfrog /mrfrog
   chmod 750 /mrfrog
   ```
   `chown` 命令将用户和组所有权设置为 `mrfrog` 的用户和组。`chmod` 命令使 `/mrfrog` 目录仅对 `mrfrog` 用户和组可访问。
   ```bash
   chown -R root.root /mrfrog/etc /mrfrog/bin /mrfrog/lib
   ```
   此命令将 `/mrfrog` 下 `etc`、`bin` 和 `lib` 子目录的所有权更改为 `root` 用户和组。
   ```bash
   cd /mrfrog
   chmod -R 111 *
   ```
   第一个命令将目录更改为 `/mrfrog`，第二个命令使所有文件和目录对所有人都只有可执行权限。
   ```bash
   cd etc; chmod 444 *
   ```
   这些命令将目录更改为 `/mrfrog/etc` 目录，并将文件权限更改为对所有人都只读。

