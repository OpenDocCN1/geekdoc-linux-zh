

在我的 Apache 服务器上，我仅将 cgi 扩展名指定为 CGI 脚本；因此，我将 CgiWrap 可执行文件重命名为 cgiwrap.cgi 以使其正常工作。如果你也有类似的限制，可以尝试这种方法，或者创建一个链接。

现在，按照以下方式执行 CGI 脚本：

```
http://www.yourdomain.com/cgi-bin/cgiwrap/username/scriptname
```

例如，要访问 wormhole.nitec.com 网站上用户 kabir 的 CGI 脚本 test.cgi，我会使用以下地址：

```
http://wormhole.nitec.com/cgi-bin/cgiwrap/kabir/test.cgi
```

如果你想查看 CGI 的调试输出，请指定使用 cgiwrapd 而不是 cgiwrap，如下面的 URL 所示：

```
http://www.yourdomain.com/cgi-bin/cgiwrapd/username/scriptname
```

如果该脚本是 nph 风格的脚本，你必须使用以下 URL 来运行它：

```
http://www.yourdomain.com/cgi-bin/nph-cgiwrap/username/scriptname
```

## 隐藏关于 CGI 脚本的线索

当破坏者扫描网站以寻找可能的安全漏洞时，他们会寻找那些能揭示网站底层硬件和软件的小细节。因此，你提供的系统线索越少，你的网站成为破坏者下一个受害者的可能性就越低。有几种方法可以隐藏一些可能成为重要线索的细节。

### 使用非标准的脚本别名

使用 cgi-bin 别名非常流行。一旦看到带有 cgi-bin 的 URL，你就知道该网站运行某种 CGI 脚本。此别名是在 Apache 的 httpd.conf 文件中通过 ScriptAlias 指令设置的。例如：

```
ScriptAlias "/cgi-bin/" "/path/to/real/cgi/directory/"
```

但很少有人意识到，你可以使用任何内容来创建这样的别名。例如：

```
ScriptAlias "/apps/" "/path/to/real/cgi/directory/"
```

现在，URL 中的 apps 起到了与 cgi-bin 相同的作用。因此，如果你使用类似于以下的内容：

```
ScriptAlias "/dcon/" "/path/to/real/cgi/directory/"
```

这无疑会混淆一些破坏者，因为 dcon（或者你实际使用的任何名称）是非标准的。此外，请记住许多破坏者使用自动程序来扫描网站的功能和其他线索。像上面这样的非标准脚本别名不太可能被纳入任何自动程序中。

## 为 CGI 脚本使用无扩展名名称

许多网站大胆地展示它们运行什么类型的 CGI 脚本。例如：

```
http://www.domain.com/cgi-bin/show-catalog.pl
```

上述 URL 提供了关于该网站的两个线索。首先，它告诉我们该网站支持 CGI 脚本；其次，该网站将 Perl 脚本作为 CGI 脚本运行。如果上述网站改为使用：

```
http://www.domain.com/ext/show-catalog
```

则更难确定该网站的任何信息。应避免使用 .pl 或 .cgi 扩展名，因为这些扩展名会提供有关你系统的线索。要将现有脚本的扩展名从 .pl、.cgi 等更改为无扩展名，只需重命名脚本即可。切换到无扩展名名称时，你不需要更改或添加任何新的 Apache 配置。

与 CGI 脚本类似，SSI 脚本也带来一些安全风险。下文将对此进行讨论。

## 使用 CGI 扫描器

CGI 扫描器用于扫描 Web 服务器中与 CGI 脚本相关的漏洞。我喜欢两个扫描器：cgichk.pl 和 Whisker。

### cgichk.pl

这是一个用 Perl 编写的简单 CGI 扫描器。你可以从 www.packetstormsecurity.com 下载源代码。使用 `perl cgichk.pl` 命令从命令行运行时，它会要求你输入要扫描的 Web 服务器的主机名和端口号（默认 80）。你还可以选择将结果记录到文件中。

cgichk.pl 首先检查 Web 服务器使用的 HTTP 协议版本。例如，以下示例会话显示 cgichk.pl 正在扫描名为 rhat.nitec.com 的主机。

```
CGI scanner [in Perl] v1.1
Host: rhat.nitec.com
HTTP Port [80]:
Log Session? (y/n)
Log File [rhat.nitec.com.scan]:
```

```
Press [Enter] to check the httpd version...

HTTP/1.1 200 OK
Date: Tue, 27 Mar 2001 04:50:47 GMT
Server: Apache/2.0.14 (Unix)
Last-Modified: Mon, 26 Mar 2001 20:23:13 GMT
ETag: "1ba42-1000-c65eee40"
Connection: close
Content-Type: text/html; charset=ISO-8859-1
```

检测到协议版本后，cgichk.pl 将要求你按回车键以开始检查 CGI 漏洞。以下输出是在运行 Apache 2.0 的 rhat.nitec.com Web 服务器上扫描 CGI 安全问题的示例。

```
Searching for /cgi/ - backdoor    : Not Found
Searching for /TC - backdoor       : Not Found
Searching for phf                  : Not Found
Searching for Count.cgi            : Not Found
Searching for test.cgi             : Not Found
Searching for nph-test-cgi         : Not Found
Searching for nph-publish          : Not Found
Searching for php.cgi              : Not Found
Searching for handler              : Not Found
Searching for webgais              : Not Found
Searching for websendmail          : Not Found
Searching for webdist.cgi          : Not Found
Searching for faxsurvey            : Not Found
Searching for /htmlscript          : Not Found
Searching for /per/displpay        : Not Found
Searching for perl.exe             : Not Found
Searching for wwwboard.pl          : Not Found
Searching for www-sql              : Not Found
Searching for /view-source         : Not Found
Searching for campas               : Not Found
Searching for /gl1mpse             : Not Found
Searching for gl1mpse              : Not Found
Searching for /nirw.man.sh         : Not Found
Searching for AT-admin.cgi         : Not Found
Searching for /filenaill.pl        : Not Found
Searching for /mailist.pl          : Not Found
Searching for /jj                  : Not Found
Searching for info2www             : Not Found
Searching for /files.pl            : Not Found
Searching for finger               : Not Found
Searching for /bninorm.cgi         : Not Found
Searching for /survey.cgi          : Not Found
Searching for /AnycForm2           : Not Found
Searching for txtcounter.pl        : Not Found
Searching for /classfields.cgi     : Not Found
Searching for /eniron.cgi          : Not Found
Searching for /wrup                : Not Found
Searching for /cglwrap            : Not Found
Searching for guestbook.cgi        : Not Found
```

```
Searching for edit.pl : Not Found
Searching for perlshop.cgi : Not Found
Searching for anyboard.cgi : Not Found
Searching for webbbs.cgi : Found!
Searching for environ.cgi : Not Found
Searching for whois_raw.cgi : Not Found
Searching for _vti_inf.html : Not Found
Searching for service.pwd : Not Found
Searching for users.pwd : Not Found
Searching for authors.pwd : Not Found
Searching for administrators : Not Found
Searching for shtml.dll : Not Found
Searching for shtml.exe : Not Found
Searching for args.bat : Not Found
Searching for uploader.exe : Not Found
Searching for rguest.exe : Not Found
Searching for wguest.exe : Not Found
Searching for bd1r - samples : Not Found
Searching for CGImail.exe : Not Found
Searching for newsn.exe : Not Found
Searching for fpcount.exe : Not Found
Searching for counter.exe : Not Found
Searching for visadmin.exe : Not Found
Searching for openfile.cfm : Not Found
Searching for expcalc.cfm : Not Found
Searching for disposedfile : Not Found
Searching for sendmail.cfm : Not Found
Searching for codebrws.asp : Not Found
Searching for codebrws.asp 2 : Not Found
Searching for showcode.asp : Not Found
Searching for search97.vts : Not Found
Searching for carco.dll : Not Found
Server may have CGI vulnerabilities.
```

注意加粗的那一行。扫描发现了一个潜在的 CGI 安全风险。webbbs.cgi 脚本可能被脚本小子和想当黑客的人滥用来入侵系统。如果你的扫描识别出一个或多个安全风险，请考虑删除这些脚本或使用适当的修复方法更新它们。

### Whisker

Whisker 是一个基于 Perl 的 CGI 扫描器，我非常喜欢它。你可以从 www.filesearch.ru 下载源发行版。下载后，在目录中提取源代码，并运行 whisker.pl 脚本，命令为 `perl whisker.pl -h hostname`。例如，`perl whisker -rh at.nitec.com` 命令会在名为指定主机的 Apache Web 服务器上运行扫描器。结果如下所示：

```
Host: rhat.nitec.com
= Server : Apache/2.0.14 (Unix)
+ 200 OK: HEAD /cgi-bin/webbbs.cgi
+ 200 OK: HEAD /manual/
+ 200 OK: HEAD /temp/
```

