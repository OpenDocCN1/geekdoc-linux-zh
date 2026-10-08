
手动完成后执行。最好与目标应用程序保持相同的目录结构。
例如：

```
www.victim.com
/admin/admin.html
/main/index.html
/menu/menu.asp
```

## 手动检查应用程序

调查应用程序的最佳方法是实际上点击你能找到的每一个链接，并将每个页面的信息记录在攻击矩阵中。手动分析是极其费力的，但严谨的安全审查需要与应用程序进行交互。在浏览览应用程序时，请留意不同类型的信息：

- 静态和动态生成的页面
- 目录结构
- 辅助文件
- Java 类和 applet
- HTML 注释和内容
- 表单
- 查询字符串 (Query strings)
- 反向连接 (Back-connectivity)

第一步是访问应用程序并确定使用了哪些身份验证方法（如果有）。我们将在第 5 章中详细讨论身份验证，但现在重要的是识别出该方法。此外，仅仅因为 /main/login.jsp 页面需要身份验证，/main/menu.jsp 页面可能不需要。这就是配置错误开始显现的步骤。

## 静态和动态生成的页面

静态页面通常是被归类到常见问题解答（FAQs）和联系信息的 .html 文件。它们可能缺乏通过验证测试进行攻击的功能，但 HTML 源代码可能包含某些内容或信息。至少，联系信息会泄露电子邮件地址和用户名。动态生成的页面（.asp, .jsp, .php 等）更有趣。对于一些有趣的页面，如管理员功能、用户资料信息或购物车视图，请阅读其简短注释。

将文件保存到磁盘。同时，维护应用程序的目录结构。如果 www.victim.com 有一个 /include/database.inc 文件，则创建一个名为 "www.victim.com" 的顶层目录和一个名为 "include" 的子目录，并将 "database.inc" 文件放置在 include 目录中。文本浏览器 lynx 可以加速这一过程：

## 第 4 章：调查应用程序

```
[root@meddle] # mkdir www.victim.com
[root@meddle] # cd www.victim.com
[root@meddle www.victim.com]# lynx -dump www.victim.com/index.html > index.html
```

netcat 更好，因为它还会转储服务器头信息：

```
[root@meddle] # mkdir www.victim.com
[root@meddle] # cd www.victim.com
[root@meddle www.victim.com]# echo -e "GET /index.html HTTP/1.0\n\n" | \
nc -vv www.victim.com 80 > index.html
www.victim.com [192.168.33.101] 80 (http) open
sent 27, rcvd 2683: NOTOCK
```

为了进一步自动化该过程（懒惰是不存在的！），为 netcat 创建一个包装脚本。该脚本可以在 UNIX 和安装了 Cygwin 工具的 Windows 系统上运行。创建一个名为 "getit.sh" 的文件并将其放入执行路径中：

```bash
#!/bin/sh
# mike's sgetit.sh script
if [ -z $1 ]; then
  echo -e "\nUsage: $0 <host> <URL>"
  exit
fi
echo -e "GET $2 HTTP/1.0\n\n" | \
nc -vv $1 80
```

等一下！lynx 和 Mozilla 可以处理仅通过 SSL 的页面。你可以用 netcat 做同样的事情吗？简单回答是：不能。但是，你可以使用 OpenSSL 包。创建一个名为 "sgetit.sh" 的第二个文件并将其放入执行路径中：

```bash
#!/bin/sh
# mike's sgetit.sh script
if [ -z $1 ]; then
  echo -e "\nUsage: $0 <SSL> <URL>"
  exit
fi
echo -e "GET $2 HTTP/1.0\n\n" | \
openssl s_client -quiet -connect $1:1443 2>/dev/null
```

"getit" 脚本的多功能不仅限于两个命令行参数。你可以构建它们来添加 cookie、user-agent 字符串、主机字符串或任何其他 HTTP 头部。你只需要修改 "echo -e" 这一行。

## 破解暴露的 Web 应用程序

现在你正在命令行中使用 HTTP 和 HTTPS 工作。应用程序将会崩溃的！因此，与其从浏览器中保存每个文件或运行 lynx：

```
[root@meddle]# # mkdir www.victim.com
[root@meddle]# # cd www.victim.com
[root@meddle:www.victim.com]# # get.sh www.victim.com /index.html > index.html
www.victim.com [192.168.33.101] 80 (http) sent 27, rcvd 2683: NOTSOCK
[root@meddle:www.victim.com]# # mkdir secure
[root@meddle:www.victim.com]# # cd secure
[root@meddle:secure]# # get.sh www.victim.com /secure/admin.html > admin.html
```

get.sh 最后一行的 "/dev/null" 抑制了连接和错误信息。"s_client" 比 netcat 详细得多。（此处省略了原文中大量重复的无效描述）。这就是配置错误开始显现的步骤。
