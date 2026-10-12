
## 降低 CGI 风险

Web 上最大的安全风险以 CGI 应用程序的形式出现。CGI 本身并不不安全，但编写糟糕的 CGI 应用程序是 Web 安全漏洞的主要来源。实际上，CGI 规范的简单性使得许多缺乏经验的程序员能够轻松编写 CGI 应用程序。这些缺乏经验的程序员不了解互联网网络的安全方面，创建的应用程序虽然能运行，却也在运行这些应用程序的系统上制造了隐藏的后门和漏洞。

以下是 CGI 应用程序可能造成的三种最常见的安全风险：

- **信息泄露。** 此类泄露帮助黑客入侵系统。黑客了解的系统信息越多，入侵系统就越容易。
- **通过 CGI 应用程序执行系统命令。** 在许多情况下，远程用户成功诱骗基于 HTML 表单的邮件脚本运行系统命令或泄露机密系统信息。
- **消耗系统资源。** 编写糟糕的 CGI 应用程序可能会消耗系统资源，导致服务器几乎无响应。

当然，当您的 Apache 服务器以非特权用户身份运行这些应用程序时，您应该在开发或安装 CGI 应用程序时采取谨慎的步骤，但即使编写仔细的应用程序也可能成为安全风险。CGI 应用程序造成的大多数安全漏洞都是由用户输入引起的。

### 使用包装器限制 CGI 风险

降低 CGI 相关风险的最佳方法是根本不运行任何 CGI 应用程序；然而，在动态 Web 内容的时代，这不切实际。也许您可以将所有 CGI 应用程序集中在一个位置，并密切监控其开发，以确保它们编写良好。

在许多情况下，特别是在 ISP 系统上，所有拥有网站的用户都想要 CGI 访问权限。在这种情况下，以拥有 CGI 应用程序的用户的 UID 运行 CGI 应用程序可能是个好主意。默认情况下，在 Apache 上运行的 CGI 应用程序使用 Apache UID。如果您使用所有者的 UID 运行这些应用程序，所有可能的损害将仅限于该 UID 被允许访问的内容。换句话说，使用除 Apache 服务器 UID 以外的 UID 运行的不良 CGI 应用程序只能损坏用户的文件。负责 CGI 应用程序的用户现在可以更加小心，因为可能的损害将仅影响其自己的内容。一举两得，您获得了更高的用户责任感和意识，同时也限制了潜在损害的范围。要使用 Apache 服务器使用的 UID 以外的 UID 运行 CGI 应用程序，您需要一种称为包装器的特殊程序，它允许您以拥有该文件的用户身份运行 CGI 应用程序，而不是作为 Apache 服务器用户。一些 CGI 包装器在运行请求的 CGI 应用程序之前会进行其他安全检查。以下部分介绍两种流行的 CGI 包装器。

#### suEXEC

Apache 自带一个名为 suEXEC 的支持应用程序，它为 Apache 用户提供了以不同于 Apache UID 的 UID 运行 CGI 和 SSI 程序的能力。suEXEC 是一个 setuid 包装器程序，当对管理员指定的以不同于 Apache 服务器 UID 的 UID 运行的 CGI 或 SSI 程序发出 HTTP 请求时，会调用该程序。发出此类请求时，Apache 会向 suEXEC 包装器提供程序名称、UID 和 GID。suEXEC 使用给定的 UID 和 GID 运行程序。

在运行 CGI 或 SSI 命令之前，suEXEC 包装器会执行一组测试以确保请求有效。除其他事项外，此测试过程确保 CGI 脚本由被允许运行包装器的用户拥有，并且 CGI 目录或 CGI 脚本仅可由所有者写入。安全检查成功后，suEXEC 包装器分别通过 setuid 和 setgid 调用将 UID 和 GID 更改为目标 UID 和 GID。组访问列表也会初始化为用户所属的所有组。suEXEC 通过建立安全的执行 PATH（在配置期间定义），以及仅传递安全环境列表中列出的变量名（也在配置期间创建），来清理进程的环境。然后 suEXEC 进程成为目标 CGI 应用程序或 SSI 命令并执行。这似乎需要做很多工作——确实如此——但这也提供了更高的安全系数。

如果您有兴趣在 Apache 中安装 suEXEC 支持，请按如下方式运行 configure（或 config_status）脚本：

```
./configure --prefix=/path/to/apache \
--enable-suexec \
--suexec-caller=httpd \
--suexec-userdir=public_html \
--suexec-uidmin=100 \
--suexec-gidmin=100 \
--suexec-safepath="/usr/local/bin:/usr/bin:/bin"
```

以下是此配置的详细说明：

- **--enable-suexec.** 启用 suEXEC 支持。
- **--suexec-caller=httpd.** 将 *httpd* 更改为您在 Apache 配置文件中 User 指令使用的 UID。这是唯一被允许运行 suEXEC 程序的用户。
- **--suexec-userdir=public_html.** 定义用户主目录下存放 suEXEC 可执行文件的子目录。将 *public_html* 更改为您用作 UserDir 指令值的任何内容，该指令指定用户网站的文档根目录。
- **--suexec-uidmin=100.** 定义允许运行基于 suEXEC 的 CGI 脚本的最低 UID。换句话说，低于此数字的 UID 将无法通过 suEXEC 运行 CGI 或 SSI 命令。查看您的 /etc/passwd 文件，确保您选择的范围不包括通常低于 100 的系统账户。
- **--suexec-gidmin=100.** 定义允许作为目标组的最低 GID。换句话说，低于此数字的 GID 将无法通过 suEXEC 运行 CGI 或 SSI 命令。查看您的 /etc/group 文件，确保您选择的范围不包括通常低于 100 的系统账户组。
- **--suexec-safe-path="/usr/local/bin:/usr/bin:/bin".** 定义 suEXEC 为 CGI 应用程序和 SSI 命令执行的 PATH 环境变量。

在您将 suEXEC 包装器和新的 Apache 可执行文件安装到适当位置后，重启 Apache，它将写入类似如下的消息：

```
[notice] suEXEC mechanism enabled (wrapper: /usr/local/sbin/suexec)
```

这表明 suEXEC 已激活。现在，测试 suEXEC 的功能。在 `srm.conf` 文件中，添加以下行：

```
UserDir public_html
AddHandler cgi-script .pl
```

第一条指令（`UserDir`）将用户网站的文档根目录设置为 `~username/public_html`，其中 `username` 可以是系统上的任何用户。第二条指令将 cgi-script 处理程序与 `.pl` 文件关联。这样做是为了将扩展名为 `.pl` 的 Perl 脚本作为 CGI 脚本运行。对于此测试，您需要一个用户账户。在本示例中，我将使用主机 `wormhole.nicee.com` 和一个名为 `kabir` 的用户。将清单 12-2 中所示的脚本复制到一个名为 `test.pl` 的文件中，并将其放在用户的 `public_html` 目录中。在我的情况下，我将文件放在 `~kabir/public_html` 目录中。

### 清单 12-2：用于测试 suEXEC 支持的 CGI 脚本

```
#!/usr/bin/perl

#
# Make sure the preceding line is pointing to the
# right location. Some people keep perl in
# /usr/local/bin.

my ($key,$value);
print "Content-type: text/html\n\n";
print "<h1>Test of suEXEC<h1>";

foreach $key (sort keys %ENV){
  $value = $ENV{$key};
  print "$key = $value <br>";
}
exit 0;
```

要通过 Web 浏览器访问该脚本，我请求以下 URL：
`http://wormhole.nitec.com/~kabir/test.pl`

CGI 脚本只有在通过 suEXEC 执行的所有安全检查后才会执行。suEXEC 还会在其日志文件中记录脚本请求。我的请求的日志条目如下：

`[2000-12-01 16:09:22] aid: (kabir/kabir) gid: (kabir/kabir) cmd: test.pl`

如果您真的想知道脚本是否在用户的 UID 下运行，请在 foreach 循环中插入一个 sleep 命令（如 `sleep(10);`）。这将减慢执行速度，并允许您在 Web 服务器控制台上运行 `top` 或 `ps` 等命令，以找出运行 `test.pl` 的进程的 UID。您也可以使用 chown 命令更改脚本的所有权。尝试通过 Web 浏览器访问该脚本，并查看 suEXEC 记录的错误消息。例如，当我按如下方式更改 `~kabir/public_html` 目录中 `test.pl` 脚本的所有权时，

`chown root test.pl`
