

cp testcert.cert /etc/apache/ssl.crt/testcert.crt

cp testcert.key /etc/apache/ssl.key/testcert.key

然后，创建一个目录来存放你的新 SSL 网站：

mkdir -p /wwwssl

你可以使用任何喜欢的路径，甚至是现有的路径——请记住或写下你使用的路径，因为在稍后配置 Apache 时你会需要它。

最后，创建一个简单的信息文件，以便在测试 SSL 时有所展示：

echo "<?php phpinfo(); ?>" > /wwwssl/index.php

现在你的密钥已就位，SSL 网站根目录已创建，你需要在 httpd.conf 中启用 SSL 功能。如果你当前的 httpd.conf 文件包含一行写着“Include /etc/apache/ssl.conf”或类似的内容，那么任何 SSL 更改都应该在指定的 ssl.conf 文件中执行。否则，你可以直接在 httpd.conf 文件中进行修改，或者添加你自己对 ssl.conf 文件的引用，并在那里进行修改。

在你的 SSL 配置文件或配置段中，你需要确保以下项在全局配置作用域中可用（而不是在虚拟服务器或目录配置段中）：

Listen 443

接下来，你需要重用现有的 VirtualHost 段来处理 443 端口（如果存在），或者创建一个新的段，其中包含以下指令：

<VirtualHost _default_:443>

# Server Certificate:
SSLCertificateFile /etc/apache/ssl.crt/testcert.crt

# Server Private Key:
SSLCertificateKeyFile /etc/apache/ssl.crt/testcert.key

SSLEngine On

DocumentRoot "/wwwssl" # 使用你之前创建的 SSL 目录

Servername www.example.com
ServerAdmin youremail@example.com

</VirtualHost>

然后，一旦对配置文件进行了更改，请重启 Apache。如果你在浏览器中使用 https:// URL（例如 https://www.example.com）加载你的新 SSL 站点，你会收到证书无效的提示（因为它是自签名的）。点击“确定”，你应该能看到 phpinfo() 函数的输出。如果没有显示任何内容，或者浏览器无法连接到服务器，请检查 Apache 错误日志中是否有相关的错误消息——很可能只是一个简单的拼写错误。

> 要进一步调整 mod_ssl，并获取可用于 mod_ssl 的所有配置指令的完整列表，请访问 [http://httpd.apache.org/docs/2.0/mod/mod_ssl.html](http://httpd.apache.org/docs/2.0/mod/mod_ssl.html)。

## Apache 作为文件仓库

使用 Apache 比较酷的功能之一是将其用作简单的在线文件仓库，通过 WebDAV 实现。WebDAV（Web 分布式创作和版本控制）使 Apache 能够让用户将启用的目录视为其计算机上的远程目录或驱动器。类似于 Windows 共享或 NFS 导出，WebDAV 允许远程编辑和存储访问，只是使用 HTTP 作为传输层，而不是像 SMB 和 NFS 那样使用专门的 TCP 协议或端口。

要理解 WebDAV 如何作为共享驱动器工作，直接查看其实际运行过程会更容易理解，因此接下来，你将启用随 Apache 提供的 mod_dav 并进行测试。首先，与其他模块一样，检查 mod_dav 是否已经静态编译到 Apache 中，或者是否存在为可加载模块：

/path/to/httpd -l
ls /path/to/apache/modules

正如你可能猜到的那样，如果在 `httpd -l` 输出中没有看到 `mod_dav.c`，或者在文件列表中没有看到 `mod_dav.so`，你需要使用 Apache httpd 源代码自行构建它。要将 mod_dav 静态添加到 Apache 二进制文件中，请确保 configure 命令中存在 `--enable-dav` 和 `--enable-dav-fs`：

./configure \
--enable-dav \
--enable-dav-fs \
# ...以及你使用的其他 configure 设置

要将 mod_dav 构建为共享对象，只需在两个 DAV 相关行的末尾添加 `shared`：

./configure \
--enable-dav=shared \
--enable-dav-fs=shared \
# ...以及你使用的其他 configure 设置

然后使用 `make` 和 `make install` 构建并安装新的二进制文件和模块。

如果你决定使用 mod_dav 的动态模块，你需要在 httpd.conf 中启用它们，使用以下行：

LoadModule dav_module modules/mod_dav.so
LoadModule dav_fs_module modules/mod_dav_fs.so

为了实际存储 WebDAV 文件仓库的位置，你可以创建一个新目录，或者使用你选择的现有目录。你应该将 WebDAV 文件夹放在启用了 SSL 的网站根目录中，或者如果你计划使用基本身份验证来限制对 WebDAV 文件夹的访问，请确保稍后启用 SSL。基本身份验证以明文发送用户名和密码，因此你希望启用受保护目录的 SSL，以加密基本身份验证请求。如果需要，创建新的文件夹，并创建一个临时文件添加到 WebDAV 文件夹中：

mkdir -p /wwwssl/dav
echo "Testing DAV" > /wwwssl/dav/testing.txt

当用户访问你的 WebDAV 文件夹时，你将通过数据库或 htpasswd 文件对他们进行身份验证，以防止互联网上的匿名用户占满你的硬盘。首先，创建一个 htpasswd 文件来存储有效用户的密码，并使用 testdav 的用户账户对其进行初始化：

mkdir -p /davauth
/path/to/htpasswd -c /davauth/dav.htpasswd testdav

当提示输入密码时，输入你选择的密码。接下来，在 /wwwssl/dav 文件夹中创建一个 `.htaccess` 文件以强制执行基本身份验证。`.htaccess` 文件应包含以下内容：

AuthName "DAV Test"
AuthType Basic
AuthUserFile "/davauth/dav.htpasswd"
require valid-user

最后，在你的 httpd.conf 中创建一个 Directory 条目，以启用给定目录的 WebDAV 和基本身份验证：

<Directory "/wwwssl/dav">
    AllowOverride AuthConfig
    Dav On
</Directory>

然后你可以重启 Apache，WebDAV 将为你的 HTTPS 站点的 /dav/ 文件夹启用，可以通过类似 https://www.example.com/dav 的地址访问。你可以尝试在 Web 浏览器中加载此 URL，但其行为与普通非 DAV 网络目录没有区别。要使用你的 WebDAV URL 的功能，你需要使用支持 WebDAV 的软件。

jEdit、NuSphere 的 PHPEd 和 Macromedia Dreamweaver 等编辑器以及其他编辑器在一定程度上都支持 WebDAV。如果你手头没有这些编辑器，请不要担心——大多数现代操作系统实际上都支持在其文件资源管理器/浏览器工具中原生挂载 WebDAV 共享。

要使用操作系统的文件浏览器访问你的 WebDAV 共享，请按照适用于你操作系统的上述部分中的说明进行操作。

### Windows 2000/XP

要在 Windows 2000 或 XP 下设置 WebDAV，你需要按照以下顺序运行“添加网络位置”向导：

- 1. 转到“我的网络位置”，双击“添加网络位置”，如 6.1 图所示。
- 2. 当出现“添加网络位置向导”时，单击“下一步”以显示服务提供商列表。选择“选择其他网络位置”选项，如 6.2 图所示，然后单击“下一步”。

# 第 6 章

![](img/ab27c6ac898db1f934d39fa127b14657_185_0.png)

图 6.1

![](img/ab27c6ac898db1f934d39fa127b14657_185_1.png)

图 6.2

- 3. 在“Internet 或网络地址”字段中输入你的 WebDAV 目录的 URL，如 6.3 图所示。然后单击“下一步”。

![](img/ab27c6ac898db1f934d39fa127b14657_186_0.png)

图 6.3

- 4. 在 SSL 安全警报对话框中单击“是”。之所以发出警告，是因为你使用的是自签名证书——这与之前尝试访问启用 SSL 的网站时看到的警告相同。
- 5. 然后系统会提示你输入用户名和密码以访问 DAV Test 域。输入创建 .htpasswd 文件时使用的值。
- 6. 然后系统提示你为网络位置命名，以便稍后轻松识别该位置。将网络位置的名称输入为 **My WebDAV**。
- 7. 现在你的 WebDAV 位置应该设置好了，你将看到“完成添加网络位置向导”屏幕。勾选“当我点击完成时打开此网络位置”复选框，如 6.4 图所示。
- 8. 然后系统会再次提示你接受自签名 SSL 证书并输入用户名和密码。接受该证书并输入你在第 5 步中使用的凭据。
- 9. 然后你应该会在标准的 Windows 资源管理器窗口中看到 WebDAV 共享的内容，如 6.5 图所示。
- 10. 像标准驱动器或文件夹一样使用你的 My WebDAV 共享——你可以像操作本地文件夹一样在 WebDAV 共享中添加、编辑和删除文件。

