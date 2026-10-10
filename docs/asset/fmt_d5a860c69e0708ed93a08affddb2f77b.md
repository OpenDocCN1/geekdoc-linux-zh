
```bash
$ ls _DAP-1320_FIRMWARE_1.11B10.zip.extracted/
DAP1320_fw_11b10.bin.extracted/
```
现在包已经提取完成，接下来是浏览文件，寻找功能、配置或未知应用程序。表 21-1 定义了一些在浏览时需要查找的项目：

| it | Bash 命令示例 |
| --- | --- |
| 定位可执行文件（注意：BusyBox 文件）。 | `find . -type f -perm /u+x` |
| 为后续分析确定目录结构。 | `find . -type d` |
| 查找 Web 服务器或相关技术。 | `find . -type f -perm /u+x -name "*http*" -name "*cgi*" -o name "*nginx*"` |
| 查找库版本。 | `for i in `find . -type d -name lib`; do find $i -type f; done` |
| 查找 HTML、JavaScript 和配置文件。 | `find . -name "*.html" -o name "*.js" -o name "*.cgi" -o name "*.conf"` |
| 查看可执行版本（例如，lighttpd）。 | `strings bin/lighttpd | grep lighttpd` |

# 文件系统示例

**注意** 找到每个可执行文件或库都需要与已知漏洞进行交叉检查。例如，使用 Google 搜索 `<name> <version number> vulnerability`。

一旦你收集了所有这些信息，你将想要了解浏览器或任何运行的服务是如何处理请求的。由于我们已经执行了前面的，我们简化了下面的示例以使分析更加直接。发现 Web 服务器是 `lighttpd` 1，它使用 `lighttpd*.conf` 2 和 `modules` 3 进行配置。此外，它使用 `cgi.conf` 4，该文件将几乎所有的处理都指向 `/bin/ssi` 5（一个二进制可执行文件）。

```bash
