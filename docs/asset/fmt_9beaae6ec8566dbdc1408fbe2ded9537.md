
$data = shift;

$secret = 'ID10t'; # 如果愿意，可以更改此密钥。

# 我们需要以下行来告诉 Perl

```
# 370 第四部分：网络服务安全

# 列表 15-2（续）
```

```perl
# 我们想使用 Digest::MD05 模块。

use Digest::MD05;

# 创建一个新的 MD05 对象

my $ctx = Digest::MD05->new;

# 添加数据

$ctx->add($data);

# 添加密钥

$ctx->add($secret);

# 创建 Base64 摘要

my $digest = $ctx->b64digest;

# 返回摘要

return $digest;

}
```

```perl
sub alert(

#

# 目的：使用 JavaScript
#    显示警报框
#

# 获取我们需要显示的消息

my $msg = shift;

# 创建使用 JavaScript alert()
# 对话框函数来显示消息，
# 然后将浏览器返回到上一个屏幕

print <<JAVASCRIPT;

<script language="JavaScript">

alert($msg);

history.back();

</script>

JAVASCRIPT

)
```

这是一个简单的多屏幕 CGI 脚本，它在第一个屏幕中询问用户姓名，在接后的屏幕中询问电子邮件地址，最后打印消息。当用户从一个屏幕移动到另一个屏幕时，上一个屏幕的数据会通过隐藏标签（hidden tags）传递到下一个屏幕。这就是它的工作原理。

第一个屏幕询问用户姓名。一旦用户输入了姓名，接下来的屏幕就会询问用户的电子邮件地址。HTML 源代码见列表 15-3。

## 列表 15-3：hidden-md5.eg 屏幕 2 的 HTML 源代码

```html
<!DOCTYPE HTML PUBLIC "//IETF//DTD HTML//EN">
<HTML>
<HEAD>
<TITLE>多屏幕 Web 应用程序演示</TITLE>
```
</HEAD>
<BODY>
<H2>Screen 2</H2>
<HR SIZE="0" COLOR="black">
<FORM METHOD="POST"
ENTYPE="application/x-www-form-urlencoded">
Enter email:
<INPUT TYPE="text"
NAME="email"
SIZE=30>
<INPUT TYPE="hidden"
NAME="name"
VALUE="Cynthia">
<INPUT TYPE="hidden"
NAME="digest"
VALUE="IzrSJ1LrsW1YHNfshkrW/A">
<INPUT TYPE="submit"
NAME="submit"
VALUE="Next">
</FORM>
</BODY>
</HTML
```

注意隐藏数据是使用以下行存储的：

```html
<INPUT TYPE="hidden"
NAME="name"
VALUE="Cynthia">
<INPUT TYPE="hidden"
NAME="digest"
VALUE="IzrSJ1LrsW1YHNfshkrW/A">
```

第一行隐藏数据存储了 `name=Cynthia`，第二行存储了 `digest=IzrSJ1LrsW1YHNfshkrW/A`。第二部分数据是为屏幕 1 中输入的姓名生成的消息摘要。当用户在第二个屏幕中输入电子邮件地址并继续时，将显示最终屏幕。

然而，在生成最终屏幕之前，会对姓名字段计算消息摘要，并与早先创建的摘要进行比较，以验证屏幕 1 中的姓名字段值未在脚本 2 中被修改。因为 MD5 算法会为给定的数据集创建相同的消息摘要，新旧摘要之间的任何差异都会引起警报，脚本将显示警报并拒绝完成处理。如果破坏者决定修改存储在屏幕 2 中的数据（如列表 15-3 所示），脚本将检测到该修改并显示警报。

## 第四部分：网络服务安全

### suEXEC

降低风险的最佳方法是使用 `suEXEC`。在许多情况下，`suEXEC` 允许用户以 Web 服务器以外的 UID 运行 CGI 脚本。这在需要运行具有更高权限的脚本时特别有用。

### 配置 suEXEC

`suEXEC` 程序是一个允许 Apache 以不同用户运行 CGI 脚本的模块。要使用 `suEXEC`，需要在 Apache 配置文件中对其进行配置。

# 374 第四部分：网络服务安全

`-- suexec-path="/usr/local/bin:/usr/bin"` 定义了 `suEXEC` 执行 CGI 脚本和 SSI 命令时使用的 PATH 环境变量。

### 启用和测试 SUEXEC

在正确的位置安装 `suEXEC` 包装器和新的 Apache 可执行文件后，重启 Apache，它会写入类似下面的消息：

```
[notice] suEXEC mechanism enabled (wrapper: /usr/local/sbin/suexec)
```

这告诉你 `suEXEC` 已已激活。现在，在 `httpd.conf` 文件中测试 `suEXEC` 的功能，添加以下行：

```
UserDir public_html
AddHandler cgi-script .pl
```

`UserDir` 将用户网站的文档根设置为 `~username/public_html`，其中 `username` 可以是系统上的任何用户。第二个指令将 `cgi-script` 处理器与 `.pl` 文件关联。这会将以 `.pl` 扩展名的 Perl 脚本作为 CGI 脚本运行。为此，你需要一个用户账户。在例例中，请使用主机 `wormhole.nite.com` 和名为 `kabir` 的用户。尝试将列表 15-4 的脚本作为 CGI 脚本 `test.pl`，并将其放在用户的 `~kabir/public_html` 目录中。

#### 列表 15-4：测试 suEXEC 支持的 CGI 脚本

```
#!/usr/bin/perl
# 确保前面的行指向
# 正确的位置。有些人将 perl 放在
# /usr/local/bin 中。
my ($key,$value) =
print "Content-type: text/html\n\n";
print "<h1>Test of $key</h1>";foreach $key (sort keys %ENV) {
	$value = $ENV{$key};
	print "$key<br>";
}
exit 0;
```

通过 Web 浏览器访问脚本，我请求以下 URL：

```
http://wormhole.nite.com/~kabir/test.pl
```

CGI 脚本只有在通过 `suEXEC` 执行的所有安全检查后才会执行，`suEXEC` 也会在其日志文件中记录该请求。其日志条目如下

# 第 15 章：Web 服务器安全

[200-03-07 16:00:22]: uid: (kabir/kabir) gid: (kabir/kabir) cmd: test.pl

如果你真的想知道该脚本是否在用户的 UID 下运行，请在 `foreach` 循环内部插入 `sleep` 命令 `sleep(10);`，这会减慢执行速度，并允许你在 Web 服务器控制台上使用 `top` 或 `ps` 命令找到运行 `test.pl` 进程的 UID。你还可以使用 `chown` 命令更改脚本的所有权，以便通过 Web 浏览器访问脚本，并查看 `suEXEC` 记录的错误消息。例如，当我按如下更改 `~kabir/public_html` 目录中 `test.pl` 脚本的所有权时，我得到了服务器错误：

```
chown root test.pl
```

日志显示了以下行：

```
[200-03-07 16:00:22]: uid/gid (500/500) mismatch with directory (500/500) or program (0/500)
```

在这里，程序属于 UID 0，而组仍然是 `kabir` (500)，因此 `suEXEC` 拒绝运行它，这正是它应该做的事。

为了确保 `suEXEC` 在其他目录中运行 `test.pl` 程序，我在 `~kabir/public_html` 中创建一个 `cgi-bin` 目录并将 `test.cgi` 放在该目录。在确定新目录和文件的用户组所有权设置为用户 ID `kabir` 和组 ID `kabir` 后，我通过以下命令访问脚本：

```
http://wormhole.nitec.com/~kabir/cgi-bin/test.pl
```

如果你有虚拟主机并想使用 `suEXEC` 运行 CGI 程序和/或命令，请在 `<VirtualHost>` ... 容器内部使用 `User` 和 `Group` 指令。将这些指令设置为当前 Apache 服务器未使用的用户 ID 和组 ID。如果 `<VirtualHost>` 容器只指定了其中一个或一个都没有指定，则假设用户 ID 或组 ID。
