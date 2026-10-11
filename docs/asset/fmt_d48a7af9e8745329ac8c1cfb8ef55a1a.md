
`variable`: `/variable-identifier, variable-name`.

`//{list-of-values/}, /default-value/`

```text
variable: /variable-identifier, variable-name.

/{file-containing-list-of-values/}, /default-value/
```

这些术语的含义如下：

- `variable-identifier`：变量在整个配置文件中使用的名称。
- `variable-name`：显示给用户的变量的实际名称。
- `list-of-values`：逗号分隔的待显示值列表。
- `file-containing-list-of-values`：包含可能值列表的文件。列表中的每个条目占单独一行。用户可以选择其中任意一个。应提供文件的绝对路径。
- `default-value`：变量的默认值。如果未指定，则自动设置第一个值。

# `baseurl`

`baseurl` 是放置 LXR 所需的所有脚本所依据的 URL。它应该可以通过浏览器访问。在我的配置中，它是 `http://my-ip/path/<http://localhost/lxr/http/>`。确保在末尾加上 `/`，否则最后一个目录将被忽略。

# HTML 页眉和页脚

当生成源代码的 HTML 时，LXR 可以添加页眉和页脚。在 `$INSTALLPREFIX/http/` 目录中提供了示例页眉和页脚。它们分别称为 `template-head` 和 `template-tail`。此外，通过修改 `template-dir` 文件，你还可以更改 LXR 显示文件和目录的方式。可以在 `lxr.conf` 文件中通过 `htmlhead`、`htmlmail` 和 `htmlidrop` 选项指定这些文件的位置。

# `sourceroot`

此选项告诉 LXR 在哪里查找实际的源代码。在我的情况下，它是 `/var/www/htdocs/lxr/source/glibc-2.3.5`。如果你想交叉引用多个项目，你所要做的就是创建一个指定

![](img/526fd434dcfcf1b461b94c24ea170f36_80_0.png)

包含源代码的每个目录的位置。然后，你可以将该变量的值指定为 `sourceroot`。例如，我为 `glibc-2.3.5` 和 `OpenMOSIX-2.4.26` 设置了源代码，将二者的源代码分别放置在 `/var/www/httpdocs/lxr/source` 下以其名称命名的独立目录中。在 `lxr.conf` 中，我有一行如下：

```text
variable: s, Source. (glibc-2.3.5, OpenMOSIX-2.4.26)
```

然后是：

```text
sourceroot: /var/www/httpdocs/lxr/source/$$
```

因此，会根据 `source` 变量的值自动选择相应的源代码。

# `srcrootname`

`srcrootname` 指定要显示的源代码的项目名称——例如：

```text
srcrootname: $$
```

# `incprefix`

这指定要包含在该项目中的头文件的位置。

# `dbdir`

这是 `genxref` 生成的 `fileidx` 和 `xref` 文件的位置。如果你有多个项目，请为每个项目指定独立的位置，如下所示：

```text
dbdir: /var/www/httpdocs/lxr/source/$$
```

这些是配置 LXR 时需要设置的唯一选项。此外，你可以使用 `glimpsebin` 指定 `glimpse` 二进制文件的位置。

# `glimpsebin`

`glimpse` 允许用户在源代码中搜索特定文件，并在源文件中搜索任何文本。你可以从 [webglimpse.net/trial/glimpse-latest.tar.gz](webglimpse.net/trial/glimpse-latest.tar.gz) 获取 `glimpse` 的最新版本。解压并安装它。安装好 `glimpse` 后，进入源代码安装的目录（例如 `/var/www/httpdocs/lxr/source/glibc-2.3.5`），并执行以下操作：

```bash
# glimpseindex -H ..
```

输出应该看起来像这样：

```text
This is glimpseindex version 4.18.2, 2006.

Indexing "/var/www/httpdocs/lxr/source/glibc-2.3.5" ... 

Size of files being indexed = 8171416 B, Total #of files = 10075 

Index-directory: "/var/www/httpdocs/lxr/source/glibc-2.3.5" 

Glimpse-files created here:
```

![](img/526fd434dcfcf1b461b94c24ea170f36_81_0.png)

```text
-rw-r--r-- 1 root root 67398 2006-09-08 05:51 .glimpse_filenames
-rw-r--r-- 1 root root 40300 2006-09-08 05:51 .glimpse_filenames_index
-rw-r--r-- 1 root root 0 2006-09-08 05:50 .glimpse_filenames
-rw------- 1 root root 1783314 2006-09-08 05:51 .glimpse_index
-rw-r--r-- 1 root root 886 2006-09-08 05:51 .glimpse_messages
-rw------- 1 root root 836 2006-09-08 05:51 .glimpse_partitions
-rw-r--r-- 1 root root 23888 2006-09-08 05:51 .glimpse_statistics
```

这会在当前目录中创建所需的 `glimpse` 索引文件。创建完成后，确保为其他用户设置了读权限：

```bash
# chmod o+r .glimpse-*
```

现在，将 `lxr.conf` 中的 `glimpsebin` 选项设置为你安装 `glimpse` 的位置。我将其安装在 `/usr/local/sbin/glimpse`。就这样；保存并关闭文件。现在剩下的唯一任务是配置 Web 服务器以配合 LXR 工作。

# 配置 Apache

我使用的 Web 服务器是 `Apache 1.3.33`。首先要做的是设置 LXR 目录的权限。你可以通过编辑通常位于 `/etc/apache/httpd.conf` 的 `httpd.conf` 文件来完成。添加以下行：

```apache
<Directory /var/www/httpdocs/lxr>
AllowOverride All
Options All
</Directory>
```

只需将位置替换为你安装 LXR 的位置即可。

然后，进入 `$INSTALLPREFIX/http/` 目录，创建并打开一个名为 `.htaccess` 的文件进行编辑。输入以下行：

```apache
<File ~ (search|find|source|diff|ident)>
SetHandler cgi-script
</File>
```
