
## exec

`exec`指令根据你提供的参数执行 shell 命令或 CGI 程序。有效的属性有 `cgi` 和 `cmd`。
- `cgi`—要执行的 CGI 程序的 URL。该 URL 必须是本地 CGI，而不能位于其他机器上的。CGI 程序将获得最初传递给请求文档的 `QUERY_STRING` 和 `PATH_INFO`，因此指定的 URL 不能包含这些信息。你应该使用 `virtual` 代替此指令。
- `cmd`—要执行的 shell 命令。结果将显示在 HTML 页面上。

## fsize

`fsize`指令显示由 `file` 或 `virtual` 属性指定的文件的大小。大小按照 `sizefmt` 指令指定的格式显示。

- `file`—文件的路径，如果值以 `/` 开头，则相对于根目录；否则，相对于当前目录。
- `virtual`—指向文件的相对 URL 路径。

## lastmod

显示文件的最后修改日期。目标文件的指定方式与 `fsize` 指令相同。

## include

`include`指令包含文件的内容。文件通过 `file` 和 `virtual` 属性指定，与 `fsize` 和 `lastmod` 相同。

如果文件是 CGI 程序且没有设置 `IncludesNOEXEC`，则将执行程序并显示结果。这通常优于 `exec` 指令使用。你可以通过此指令传递 `QUERY_STRING`——这是使用 `exec` 指令无法做到的。

## printenv

显示所有现有变量。没有属性。例如，

```
<!--printenv -->
```

## set

使用 `set` 设置变量的值。属性为 `var`。例如，

```
<!--set var="animal" -->
```

> 注意：在 `.htaccess` 文件中，可以设置 `IncludesNOEXEC` 来禁用 SSI。

> 注意：在服务器配置文件中，可以设置这些指令。

```
config
```
