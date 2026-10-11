
`check_url=$(wget -nv -spider $quote_url 2>&1)`

现在指示器状态保存在 `check_url` 变量中。为了从 `check_url` 字符串中提取出错误指示 `error404`，可以使用参数扩展和 `echo` 命令：

```bash
bad_url=$(echo $check_url/*error404*/error404)
```

在这个示例中，字符串参数扩展允许搜索存储在 `check_url` 中的字符串。将字符串参数扩展看作是快速方便的 `sed` 替代方案。在搜索词周围使用通配符 `*error404*` 允许搜索整个字符串。如果搜索成功，`echo` 命令会将字符串 `error404` 发送到 `bad_url` 变量中进行存储。如果搜索失败，`bad_url` 变量将包含 `check_url` 的内容。

现在使用一个示例来检查 `bad_url` 变量字符串。如果找到字符串 `error404`，则显示消息并退出脚本：

```bash
if [ "$bad_url" = "error404" ]
then
  echo "Bad web address"
  echo "Quote_url invalid"
  echo "Exiting script..."
exit
```

可以使用更简单、更短的方法。这种方法完全不再需要字符串扩展和 `bad_url` 变量。双括号 `if` 语句允许对 `check_url` 变量进行搜索：

```bash
if [[ $check_url == *error404* ]]
then
  echo "Bad web address"
  echo "Quote_url invalid"
  echo "Exiting script..."
exit
```

`if` 结构内的测试语句搜索 `check_url` 变量字符串。如果在变量字符串的任何地方找到字符串 `error404`，则显示消息并退出脚本。如果指示字符串不包含错误消息，脚本将继续执行。该语句节省了时间和精力。不需要任何字符串扩展，甚至不需要 `bad_url` 变量。

现在这些已就绪，就可以用无效的网页地址测试脚本了。将 `url` 变量设置为错误的 URL 并传递给 `get_quote.sh` 脚本。

这运行得很好。为了确保一切无误，现在测试一个有效的网页地址：

```bash
$ url=www.quotationspage.com/gotd.html
./get_quote.sh $url
```

没有收到错误消息。到目前为止脚本运行得非常完美！这是需要的唯一检查，因此添加到脚本中的下一个项目是获取网页数据。

## 获取网页信息

获取每日励性名言的网页数据非常简单。脚本使用了本章之前显示的 `wget` 命令。唯一的更改是将日志文件和包含网页信息的 HTML 文件存储在 `/tmp` 目录下：

```bash
wget -o /tmp/quote.log -o /tmp/quote.html $quote_url
```

在继续处理脚本的其余部分之前，应该使用有效的网页地址测试此代码段：

```bash
$ url=www.quotationspage.com/qotd.html
$
 ./get_quote.sh $url
$
$ ls /tmp/quote.*
/tmp/quote.log /tmp/quote.html
$
$ cat /tmp/quote.html
<!DOCTYPE TYPE PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">
<html xmlns:fb="http://ogp.me/ns/fb">
<head>
[...]
<body>
</html>
$
```

脚本运行正常！文件 `/tmp/quote.log` 和 `/tmp/quote.html` 已经创建。

## 提示

如果你想在 URL 中进行检查，首先确保每日励性名言脚本的 URL 仍然有效。

正如你所做的那样，脚本使用 `wget` 和 `-spider` 选项检查网页地址的有效性。然而，生成的指示器必须保存，以便以后用 `if` 语句测试进行检查。这对于 `wget` 命令来说有一点复杂。

为了保存输出，在命令周围使用了 `$(...)` 语法。此外，还需要标准错误和标准输出重定向。这通过在 `wget` 命令末尾加上 `2>&1` 实现：

```bash
check_url=$(wget -nv -spider $quote_url 2>&1)
```

现在指示器状态保存在 `check_url` 变量中。为了从 `check_url` 字符串中提取出错误指示 `error404`，可以使用参数扩展和 `echo` 命令：

```bash
bad_url=$(echo $check_url/*error404*/error404)
```
