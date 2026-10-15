
`<html><body>Bonjour</h1></body></html>`

```bash
$ cat /var/www/html/index.html.var

URI: index.html.en

Content-Language: en

Content-type: text/html; charset=ISO-8859-1
```

```bash
URI: index.html.fr

Content-Language: fr

Content-type: text/html; charset=ISO-8859-1
```

如果你的浏览器的首选语言设置为英语 (`en`)，当你浏览到 `http://localhost/index.html.var` 时，它将显示 Hello 页面。如果你的浏览器的首选语言设置为法语 (`fr`)，它将显示 Bonjour 页面。（由于 MultiViews 选项默认是开启的，当你浏览到 `http://localhost` 时，浏览器会显示正确的页面。参见下一节。）你可以通过从菜单栏中选择“编辑+偏好”，点击“内容”图标，最后从“语言”框架中选择来更改 Firefox 中的默认语言。如有必要选择一种语言添加组合框，然后将首选语言移到列表顶部。在示例中，字符集分配是不必要的。但如果你正在使用英语、俄语等不同编码发送页面，它们将会有帮助。

`Options` 指令（第 943 页）允许 Apache 遵循符号链接，但禁止许多选项。`AllowOverride` 指令（第 945 页）导致 Apache 不处理 `.htaccess` 文件中的指令。如果你想使用限制较少的选项，则必须显式地启用它们，但这样做可能会暴露根文件系统并损害安全系统。

接下来，另一个 `<Directory>` 容器为文档根（`/var/www/html/`）设置了限制较少的选项。`httpd.conf` 中的代码中穿杂着许多注释。如果没有这些注释，它看起来像这样：

```apache
<Directory "/var/www/html">
Options Indexes FollowSymLinks
AllowOverride None
Order allow, deny
Allow from all
</Directory>
```

`Options` 指令中的 `Indexes` 选项允许 Apache 显示目录列表。`Order`（第 946 页）和 `Allow`（第 945 页）指令结合使用，允许来自所有客户端的请求。这个容器比前一个容器限制稍微少一些，尽管它不允许 Apache 遵循 `.htaccess` 中的指令。

`DirectoryIndex` 正如第 930 页所示，`DirectoryIndex` 指令导致 Apache 从请求的目录返回名为 `index.html` 的文件。由于在之前的 `<Directory>` 容器中指定了 `Options Index`，如果此文件在查询目录中不存在，Apache 将返回目录列表：

```apache
DirectoryIndex index.html index.var
```
