
# 扫描结果

Searching for `/gl1mpse`             : Not Found

Searching for `gl1mpse`              : Not Found

Searching for `/nirw.man.sh`         : Not Found

Searching for `AT-admin.cgi`         : Not Found

Searching for `/filenaill.pl`        : Not Found

Searching for `/mailist.pl`          : Not Found

Searching for `/jj`                  : Not Found

Searching for `info2www`             : Not Found

Searching for `/files.pl`            : Not Found

Searching for `finger`               : Not Found

Searching for `/bninorm.cgi`         : Not Found

Searching for `/survey.cgi`          : Not Found

Searching for `/AnycForm2`           : Not Found

Searching for `txtcounter.pl`        : Not Found

Searching for `/classfields.cgi`     : Not Found

Searching for `/eniron.cgi`          : Not Found

Searching for `/wrup`                : Not Found

Searching for `/cglwrap`            : Not Found

Searching for `guestbook.cgi`        : Not Found

```
Searching for `edit.pl` : Not Found
Searching for `perlshop.cgi` : Not Found
Searching for `anyboard.cgi` : Not Found
Searching for `webbbs.cgi` : Found!
Searching for `environ.cgi` : Not Found
Searching for `whois_raw.cgi` : Not Found
Searching for `_vti_inf.html` : Not Found
Searching for `service.pwd` : Not Found
Searching for `users.pwd` : Not Found
Searching for `authors.pwd` : Not Found
Searching for `administrators` : Not Found
Searching for `shtml.dll` : Not Found
Searching for `shtml.exe` : Not Found
Searching for `args.bat` : Not Found
Searching for `uploader.exe` : Not Found
Searching for `rguest.exe` : Not Found
Searching for `wguest.exe` : Not Found
Searching for `bd1r - samples` : Not Found
Searching for `CGImail.exe` : Not Found
Searching for `newsn.exe` : Not Found
Searching for `fpcount.exe` : Not Found
Searching for `counter.exe` : Not Found
Searching for `visadmin.exe` : Not Found
Searching for `openfile.cfm` : Not Found
Searching for `expcalc.cfm` : Not Found
Searching for `disposedfile` : Not Found
Searching for `sendmail.cfm` : Not Found
Searching for `codebrws.asp` : Not Found
Searching for `codebrws.asp 2` : Not Found
Searching for `showcode.asp` : Not Found
Searching for `search97.vts` : Not Found
Searching for `carco.dll` : Not Found
Server may have CGI vulnerabilities.
```

**注意**：扫描发现了一个潜在的 CGI 安全风险。`webbbs.cgi` 脚本可能被脚本小子和想当黑客的人滥用来入侵系统。如果你的扫描识别出一个或多个安全风险，请考虑删除这些脚本或使用适当的修复方法更新它们。

## Whisker

`Whisker` 是一个基于 Perl 的 CGI 扫描器，我非常喜欢它。你可以从 `www.filesearch.ru` 下载源发行版。下载后，在目录中提取源代码，并运行 `whisker.pl` 脚本，命令为 `perl whisker.pl -h hostname`。例如，`perl whisker -rh at.nitec.com` 命令会在名为指定主机的 Apache Web 服务器上运行扫描器。结果如下所示：

```
Host: rhat.nitec.com

= Server : Apache/2.0.14 (Unix)

+ 200 OK: HEAD /cgi-bin/webbbs.cgi

+ 200 OK: HEAD /manual/

+ 200 OK: HEAD /temp/
```

有趣的是，扫描输出使用 HTTP 状态码（如 `200`、`303`、`403` 和 `404`）来指示安全风险。例如，上述扫描结果显示在该服务器上发现了三个潜在风险（`200`）。如果你需要更多信息，请运行带有 `-i` 和 `-v` 选项的 `whisker`。例如，`perl whister.pl -h www.domain.com -i -v` 命令会在 `www.domain.com` 上运行它。以下是一个扫描输出的示例：

```
============

= Host: www.domain.com

- Directory index: /

= Server: Apache/1.3.12 (Unix) mod_oasis/5.1/

- www.apache.org

+ 302 Found: GET /scripts/

+ 403 Forbidden: GET /cgi-bin/

+ 200 OK: HEAD /cgi-bin/upload.pl

+ 403 Forbidden: HEAD /~root/

+ 403 Forbidden: HEAD /apps/

+ 200 OK: HEAD /shop/

+ 200 OK: HEAD /store/
```

请注意，有几行 `200 OK`，这意味着存在可利用的资源；`403` 表示对可利用资源的访问被拒绝，但该资源仍然存在——这既是好事也是坏事。说是好事，是因为按照服务器当前的配置，该可利用资源无法访问；但说它是坏事，是因为如果未来配置发生变化，该可利用资源可能会变得可用，这就是为什么 `403` 既是好消息也是坏消息。`302` 行表示误报。这是因为许多服务器被配置为在请求的 URL 缺失时返回自定义错误消息，从而生成 `302` HTTP 状态码。

你还可以使用 `-I n`（其中 `n` = `0` 到 `9`）选项来启用规避模式，以绕过 Web 服务器上的入侵检测系统（IDS）。如果你使用任何 IDS 解决方案，也可以测试你的 IDS 的有效性。例如，如果你的 IDS 知道 `/cgi-bin/php`（一种已知的 CGI 风险），那么使用 `-I 1` 将尝试欺骗你的 IDS，使其使用 URL 编码，从而将 `/cgi-bin/php` 请求以编码 URL 的形式发送，而不是直接在请求中使用 `/cgi-bin/php`。类似地，`-I 2` 将尝试通过在 URL 中使用额外的 `../` 模式来混淆 IDS。有关详细信息，请不带任何参数运行 `whisker`。

## 降低 SSL 风险

如果你使用 SSL 运行外部应用程序，例如使用 `exec` 命令，那么安全风险与 CGI 脚本几乎相同。然而，在 Apache 下你可以使用 `Options` 指令非常轻松地禁用此命令，如下所示：

```
<Directory />
    Options IncludesNOEXEC
</Directory>
```
