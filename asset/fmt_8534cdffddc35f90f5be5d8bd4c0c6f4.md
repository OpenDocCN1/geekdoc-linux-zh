
| 流 (Stream) | 配置文件 (Profiles) |
| :--- | :--- |
| 389-ds | 1.4 common [d] |
| an | 0.1 [d] common [d] |
| container-tools | 1.0 [d] common [d] |
| container-tools | 2.0 common [d] |
| container-tools | 3.0 common [d] |
| container-tools | 4.0 common [d] |
| eclipse | 0.10 java [d] |
| freeradium | 2.8 [d] server [d] |
| gimp | common [d], devel |
| go-tool | 0.2 [d] devel, minimal |
| httpd | common [d], common [d], dscr |
| id | 0.1 common |
| inkspace | client [d] adfrut, client |
| javapackages-runtime | 0.23 [d] common [d] |
| mc | common core |
| liblinux-python | 0.2 [d] common [d] |
| lime-toolkit | 0.8 [d] common [d] |
| log4j | 2 [d] common [d] |
| mailman | 2.1 [d] common [d] |
| mariadb | 10.3 [d] client, server [d] |
| mariadbDB | 10.5 client, server [d] |

![](img/110fa0d6324f0893fff03cee6394144d_334_0.png)

输出将继续列出一长模块列表，在最后，你将看到字母含义的键映射：

| 模块 (Module) | 版本 (Version) | 配置文件 (Profiles) |
| :--- | :--- | :--- |
| ruby | 2.2 [d] | common [d] |
| ruby | 2.6 [d] | common [d] |
| ruby | 2.7 | common [d] |
| ruby | 3.0 [d] | common [d] |
| ruby | 3.4 [d] | common [d] |
| rust-toolset | 0.1 [d] | common [d] |
| satellite-client | 0.6 [d] | common [d], gui |
| scale | 2.1 [d] | URL client packages |
| squid | 0.4 [d] | A hybrid functional/object |
| subdivision | 1.10 [d] | Apache Server |
| swig | 3.8 [d] | common [d] |
| swig | common, complete | C++/Objective C |
| varnish | 6.0 [d] | Varish HTTP cache |
| virt | 0.1 [d] | Virtualization module |

![](img/110fa0d6324f0893fff03cee6394144d_334_1.png)

这里有几个可能会引起你注意的模块：`container-tools`, `gimp`, `go-tools`, `inkscape`, `mariadb`, `mysql`, `nginx`, `nodejs`, `python`, 以及 `php`。这些都是模块，但你会注意到每个模块都有一个流（stream），该流包含一个配置文件（profile）。如果我们用图表将其视觉化，它可能会像这样：

![](img/110fa0d6324f0893fff03cee6394144d_335_0.png)

图 10.3 – AppStreams 可视化

接下来，假设我们想获取某个特定模块的信息。在这种情况下，让我们来看 `nodejs`。首先，我们在请求列表时指定 `nodejs`。我们可以通过在 `list` 命令后添加模块名称来实现，如下所示：

```bash
[root@localhost ~] dnf module list nodejs
Last metadata expiration: 0:10:45 ago on Fri 16 Dec 2022 09:29:29 PM.
Oracle Linux 8 Application Stream Profile
nodejs      10 (d) common [d], development [d]
nodejs      12 [d] development, minimal [d]
nodejs      14 [d] development, minimal [d]
nodejs      16 [d] development, minimal [d]
nodejs      18 [d] development, minimal [d]
```

在列表底部，你将看到：[d]default（默认）、[e]enabled（已启用）、installed（已安装）。由此我们可以看到流 10 被标记为 `nodejs` 的默认流 [d]。这意味着什么？基本上，如果我们运行 `dnf module install nodejs`，我们将得到流 10 中最新版本的 Node.js（且流 10 与 Node.js 相关）。

在编写本文时，流 10 中最新版本的 Node.js 是 `nodejs-10.24.0-module+e8.3.0`。我们可以通过输入以下内容来进一步深入了解这个特定的 AppStream：

```bash
# dnf module info nodejs:10
```

该命令的输出将显示流 10 中所有可用的 Node.js 版本。有很多，但为了简洁起见，我粘贴了列表最后两个：

![](img/110fa0d6324f0893fff03cee6394144d_335_png)

```text
Name : nodejs
Stream : 10 [d]
Version : 10.24.0.181969
Context : 29f0ac6
Architecture : x86_64
Profiles : common [d], development, minimal [d]
Default options : common
Repo : old_appstream
Summary : JavaScript runtime
Description : Node.js 是一个构建在 Chrome JavaScript 运行时上的平台，可以使其变得轻量化
Requires : platform[e18]
Artifacts : nodejs-10.23.1-module+e18.0+9642+879023
nodejs-10.23.1-module+e18.0+9642+879023
nodejs-docs-10.24.0-module+e18.3+9671+1543738
nodejs-full-1010.23.1-module+e18.3+9671+1543738
nodejs-nodemon-0.1.18.3-module+e18.1+5392+4d6b561f
nodejs-packaging-0.17.3-module+e18.1+5392+4d6b561f
npm:6.64.11-10.23.1-module+e18.3+9642+879023.x86_64
Name : nodejs
Stream : 10 [d]
Version : 10.24.0.2310265
Context : 29f0ac6
Architecture : x86_64
Profiles : common [d], development, minimal [d]
Default options : common
Repo : old_appstream
Summary : JavaScript runtime
Description : Node.js 是一个构建在 Chrome JavaScript 运行时上的平台，可以使其变得轻量化，但对于数据密集型应用
Requires : platform[e18]
Artifacts : nodejs-dev-10.24.0-module+e18.3+9671+1543738
nodejs-docs-10.24.0-module+e18.3+9671+1543738
nodejs-full-1010.24.0-module+e18.3+9671+1543738
nodejs-nodemon-0.1.18.3-module+e18.1+5392+4d6b561f
```
