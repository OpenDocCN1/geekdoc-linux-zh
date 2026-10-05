

## OffSec

我们将校验和和文件名一起重定向到名为 `sha256sum_nessus` 的文件中。由于 SHA256 校验和旁边的按钮仅复制校验和本身，因此我们需要手动输入文件。生成的 `sha256sum_nessus` 文件需要与 Nessus 安装包处于同一目录下。

```bash
kali@kali:~$ cd /Downloads
```

```bash
kali@kali:~/Downloads echo 498776ef9fb9bb27aa7251ab5c0529e9052778bid3aeb193917ff1f41440dd Nessus-10.5.0-debian10_amd64.deb > sha256sum_nessus
```

```bash
kali@kali:~/Downloads sha256sum -c sha256sum_nessus Nessus-10.5.0-debian10_amd64.deb: OK
```

输出显示匹配成功，我们可以安装该包。如果 Nessus 有更新版本，校验和将会不同，我们需要进行相应的调整。

要安装 Nessus 包，我们将使用带有 install 选项的 apt。

```bash
kali@kali:~/Downloads sudo apt install ./Nessus-10.5.0-debian10_amd64.deb
```

- 正在准备解压 ../Nessus-10.5.0-debian10_amd64.deb
- 正在解压 nessus (10.5)
- 正在设置 nessus (10.5.0)

正在解压 Nessus 组件...

- 你可以通过输入 `/bin/systemctl start nessusd.service` 来启动 Nessus
- 然后访问 https://kali:8834/ 来配置你的扫描器

安装完成后，我们可以通过 `systemctl` 启动 `nessusd` 服务。

```bash
kali@kali:~/Downloads sudo systemctl start nessusd.service
```

一旦 Nessus 运行，我们可以启动浏览器并导航到 https://127.0.0.1:8834。我们将看到一个指示未知证书颁发者的警告，由于使用了自签名证书，这是正常的。接受并信任该自签名证书，我们可以点击“高级...”，然后点击“接受风险并继续”。

> 305 (Man7, 2020), https://man7.org/linux/man-pages/man1/sha256sum.html

> 306 (Wikipedia, 2022), https://en.wikipedia.org/wiki/APT_(software)

> 307 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Systemd

## 使用 Kali Linux 进行渗透测试

![](img/336d6ea891e7464f18ad64426619ced4_169_0.png)

图 35：Nessus 显示证书警告

页面加载后，系统提示我们配置安装前设置。点击“继续”以默认设置开始安装。

![](img/336d6ea891e7464f18ad64426619ced4_169_1.png)

图 36：配置安装前设置

现在，我们可以选择 Nessus 产品。为了本学习单元的目的，我们将选择“注册 Nessus Essentials”并点击“继续”。

## 使用 Kali Linux 进行渗透测试

## OffSec

![](img/336d6ea891e7464f18ad64426619ced4_170_0.png)

图 37：选择 Nessus Essentials

接下来，系统提示为 Nessus Essentials 请求激活码。我们将提供所需信息并点击“注册”。

![](img/336d6ea891e7464f18ad64426619ced4_170_1.png)

图 38：请求激活码

注册完成后，激活码将在下一个窗口中显示。

![](img/336d6ea891e7464f18ad64426619ced4_171_0.png)

![](img/336d6ea891e7464f18ad64426619ced4_171_1.png)

### 图 39：激活 Nessus

接下来，我们将创建一个本地 Nessus 用户账户。我们将选择用户名 **admin** 并设置强密码，以保护你的漏洞扫描结果。我们将使用这些凭据登录 Nessus 。

![](img/336d6ea891e7464f18ad64426619ced4_171_2.png)

### 图 40：创建本地 Nessus 账户

最后，Nessus 下载并编译所有插件。这可能需要大量时间才能完成。

![](img/336d6ea891e7464f18ad64426619ced4_171_3.png)

图 41：下载 Nessus 插件

插件下载安装完成后，我们就了一个可以运行的 Nessus Essentials 实例。

### 7.2.2 Nessus 组件

在开始漏洞扫描之前，我们花点时间熟悉核心组件。当我们首次登录时，会看到一个允许我们输入目标的欢迎窗口。我们可以关闭它而不输入任何内容。

首先，让我们调查 Nessus 面板中的标签。在 Nessus 版本中，我们有两个标记为“扫描 (Scans)”和“扫描器 (Scanners)”的标签。

![](img/336d6ea891e7464f18ad64426619ced4_172_0.png)

图 42：探索 Nessus 设置

设置标签页允许我们配置全局设置。如图 42 所示，“关于”菜单允许我们自定义。现在让我们点击“策略 (Policies)”。策略是一组预定义的配置。

> 308 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Policy

> 309 (Tenable, 2022), https://docs.tenable.com/nessus/_Content/Settings

> 310 (Tenable, 2022), https://docs.tenable.com/nessus/_Content/ScanAndPolicy

## 使用 Kali Linux 进行渗透测试

## OffSec

## 交付

## 主机发现

识别网络上的主机及其开放端口。

## 漏洞扫描

![](img/336d6ea891e7464f18ad64426619ced4_173_0.png)

图 43：Nessus 策略模板

合规性 (Compliance) 类别仅适用于企业版以及移动扫描。发现 (Discovery) 类别中唯一的模板是主机发现，它可以用于创建活动主机列表。漏洞 (Vulnerabilities) 类别包含关键漏洞的模板。

Nessus 提供了三种通用扫描模板：

- 基础网络扫描 (Basic Network Scan) 使用预定义的大部分设置执行完整扫描。它将检测广泛的漏洞，因此是推荐的扫描模板。我们也可以自定义这些设置。
- 高级扫描 (Advanced Scan) 是没有预定义设置的模板。当我们想要完全自定义漏洞扫描或有特定需求时，可以使用它。
- 最后一个通用扫描模板是高级动态扫描 (Advanced Dynamic Scan)，同样没有预定义设置。这两个模板之间最大的区别在于，高级动态扫描中，我们不需要手动选择插件。该模板允许我们配置动态插件过滤器。

Nessus 插件使用攻击脚本语言 (NASL) 编写，包含检测漏洞的信息和算法。每个插件都分配给一个插件族，涵盖不同的用例。我们将在 Nessus 的最后部分使用高级动态模板和插件。

