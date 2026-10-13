
## 安装步骤

4. 如果您希望尝试最新的方法（类似于其他源代码编译过程），请留在相同的 Apache 目录中，并按顺序输入以下命令：`./configure --prefix=<prefix>`；`make`；`make install`；`<prefix>/bin/apachectl start`，其中用 Linux 文件系统路径替换 `<prefix>`，即 Apache 应安装的路径。例如，使用 `/usr/local/apache` 或 `/usr/local/etc/apache`。

5. `Configuration` 文件中可能没有太多需要更改的内容，但请仔细查看文件内容，寻找您可能希望启用的任何额外模块。

6. 在相同目录中，输入 `./Configure`。

7. 输入 `make`。

8. `make` 命令执行后，在该相同目录中会有一个名为 `httpd` 的可执行文件。通过输入 `cp httpd ../` 将该文件复制到上级的 Apache 根目录中。

9. 自定义位于 `conf/` 目录中的 `httpd.conf` 文件。您需要根据服务器的规格和需求来调整此文件。

10. 若要启动服务器，请输入以下内容（您的系统可能需要不同的命令）：`/usr/local/etc/apache/httpd -f /usr/local/etc/apache/conf/httpd.conf`。

11. 通过在浏览器中打开基础 URL 来测试系统是否正在运行。例如，对于名为 `quasi.gnuware.com` 的机器，您将在任何浏览器窗口中输入以下 URL：`http://quasi.gnuware.com/`。

12. 您还可以通过命令行输入以下命令来验证 `httpd` 守护进程是否在运行：`ps -ef | grep root | grep http`。

请记住，您的主 html 目录将不再是 `/home/httpd/html/`。如果您按照前面步骤描述的进行操作，您将发现您的根 html 目录位于 `/usr/local/etc/apache/htdocs`。

您还需要修改 `/etc/rc.d/init.d/httpd` 运行命令文件。如果您不耐烦，可以将 `apache/bin/apachectl` 文件复制到 `/etc/rc.d/init.d/` 并将其重命名为 `httpd`。您应该先备份原始文件，以防您以后决定使用旧的 RPM Web 守护进程。

在相同的根 Apache 目录中，您还会找到新的 `cgi-bin/`、`conf/` 和 `logs/` 目录。关于系统配置的更多信息，请参阅 Apache 手册页。通过遵循上述步骤，您将能够从头开始配置一个新的 Web 服务器，并根据需要编译其他模块或变量。

### 为电子商务保护 Web 服务器

如果您想通过互联网进行任何形式的安全交易，例如收集信用卡号并保护它们免受窥视，您可能需要使用 Apache 设置加密的 Web 页面。虽然您可以购买各种使您的页面*加密*或在您的 Netscape Web 浏览器上启用挂锁图标的程序，但也有一些免费模块，您可以像那样轻松地将其编译到您的 Apache Web 守护进程中。

设置安全站点可能产生的唯一成本是从两个可信来源之一购买安全证书的价格：VeriSign 和 Thawte。由于最近收购了 Thawte，VeriSign 现在控制着 95% 以上的安全证书市场。尽管这两家公司已经合并，但 Thawte 仍然提供与 VeriSign 相同质量的证书，但价格几乎是 VeriSign 的三分之一。

除了最新的 Apache 源代码外，为了启用安全的 Web 页面，你还需要以下程序：

- `OpenSSL`--0.9.5 或最新的等效版本。`OpenSSL` 最初基于 `SSLeay`（一个功能相似的程序，它也能满足需求），但现在的加密倡导者更支持 `OpenSSL`。目前可以在 `http://www.openssl.org/` 获取。

- `Apache--SSL` 或 `Apache_1.3.12*ssl_1.x`。这是一系列文件和目录，在初始编译 Apache 后放置在主 Apache 目录中。可以在 `http://apache-ssl.org/` 获取。

#### 安装 OpenSSL

要安装 OpenSSL 实用工具，请遵循以下步骤：

1. 下载 OpenSSL 的最新版本。目前最新版本是 `openssl--0.9.6`。由于开发进展迅速，此版本可能会发生变化。

2. 将文件解压到与 `apache/` 相同的目录中。虽然你可以选择其他目录，但将文件存储在此目录中比较方便。我将文件放在 `/usr/local/etc/` 中，因为这是我习惯放置早期安装的 Apache 的位置，并且我更喜欢保持自己的 `/usr/local` 目录整洁。`/usr/local` 目录是推荐用于当前 Apache 发布版本的位置。

3. 切换到刚刚创建的新 `openssl` 目录，然后输入以下命令：`./config`。

4. 输入 `make`。

5. 在安装新创建的二进制文件之前，你应该始终对其进行测试，以确保它不会破坏任何文件。输入 `make test`。

6. 如果你的二进制文件通过测试，请输入 `make install`。此命令将所有必要的文件和目录安装到 `/usr/local/ssl` 目录中。你可以通过在 `make` 命令中添加前缀来更改此选项，但始终建议使用默认值，因为开发人员大多数基于默认设置进行配置。

7. 生成一些密钥和测试 csr 文件，以生成你自己的证书或从证书颁发机构（如 VeriSign 或 Thawte）获取一个。参见以下章节了解如何生成密钥和 csr 文件。

#### 生成密钥和 csr 文件

正确安装 OpenSSL 后，你就可以开始生成密钥和 csr。你或 CA（证书颁发机构）将使用这些文件创建签名证书。

将密钥文件保存在安全的地方，因为你稍后需要它；如果你丢失了它，你将损失金钱。你应该将密钥刻录到 CD 或其他永久性存储介质上，然后将其存放在安全的地方。

要生成密钥和 csr 文件，请遵循以下步骤：

1. 输入 `cd /usr/local/ssl/private`。

2. 要生成密钥文件，请向该目录中放置大约五个简单的文本文件。它们将协助生成密钥。要创建这些文件，请输入以下内容：`/usr/local/ssl/bin/openssl genrsa -des3 -rand file1:file2:file3:file4:file5 1024 > quasi.gnuware.com.key`。此命令为名为 quasi 的服务器创建了一个密钥文件。你可以替换任何你选择的文件名。

3. 生成密钥后，将其安全地存放在安全的地方。再次强调，如果你丢失了密钥，你将损失金钱。

4. 现在创建一个 PEM 短语。这是一个识别你给服务器的个人短语或字符序列。它的作用很像任何密码，你必须输入正确的字符集才能让安全服务器启动。请妥善保管此短语。填写 csr 和启动安全守护进程时都需要它。

5. 输入 `cd ../certs`。

6. 现在创建一个 csr，你将把它提交给 CA 以获取签名证书。为此，请输入以下命令：`cd /usr/local/ssl/bin/ openssl req -new -key ../private/quasi.gnuware.com.key > quasi.gnuware.com.csr`。

7. 系统不仅会提示你输入你的 PEM 短语（一个只有你知道的唯一文本字符串），还会提示你输入关于你的公司、组织、联系人和电子邮件地址的详细信息。务必也要记录这些信息，因为如果你选择在一年后更新证书，你将需要再次准确无误地复现你在这里输入的内容。

#### 安装 Apache-SSL

要设置 Apache-SSL 模块，你必须重新编译 Apache 源代码。这是另一个建议你从源代码安装 Apache 的理由。你可以购买并安装随 Red Hat Professional 发布版本提供的最新 Apache RPM，但对于预算有限的管理员或从 Internet 下载 Red Hat 发行版的人，从源代码编译所需的程序更经济。

要配置和安装 SSL 模块，请遵循以下步骤：

1. 如前所述，正确编译 OpenSSL。

2. 下载 Apache 的最新发布版本。

3. 将 Apache 解压到不同的目录。对于常规版本，输入 `/usr/local/etc/apache/`；对于安全版本，输入 `/usr/local/etc/apache-ssl/`。

4. 输入 `cd apache-ssl/`。

5. 在新的目录 `apache-ssl/` 中解压 `apache+ssl` 文件。

6. 运行文件 `patch ./FixPatch` 并选择 `y`。

7. 确保你的 `apache+ssl` 版本与你正在运行的 Apache 发布版本相对应。如果不匹配，`FixPatch` 可执行文件将失败。

8. 输入 `cd /usr/local/etc/apache-ssl/src/`。

9. 编辑名为 `Configuration` 的文件。你在这里不需要进行太多更改。我的 `Configuration` 文件如下所示：
