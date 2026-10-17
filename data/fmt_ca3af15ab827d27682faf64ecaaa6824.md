

## 使用模板和 `makepage` 构建网站

维持严格的 Web 周期为你提供了一套可重复的流程来发布优秀的网站。然而，你仍然需要一个高度自动化且几乎不需要人工干预的内容呈现流程。

许多昂贵的软件程序声称有助于这一流程。有些人使用 Microsoft Front Page 来管理内容开发；有些人使用 Dreamweaver；有些人使用其他产品。有些人使用 Web 开发公司提供的方法，这些方法可能需要数十万美元。以下是我认为有效（并且多年来一直有效）的解决方案，用于维护从几页到几百页不等规模的网站。此解决方案的要求是：

- 创建一种简单机制，使内容作者能够发布具有统一外观和感觉的 Web 页面。
- 尽可能减少内容作者的工作量，使大部分工作自动化。
- 假设内容开发者对 HTML 知之甚少，并希望以文本格式提交内容。

为了实现这种解决方案，我编写了`makepage`，这是一个包含在此书 CD-ROM 上的脚本。该脚本使用一组 HTML 模板和一个正文（内容）页面来构建网站上的每个页面。当我开始这个项目时，我希望通过使用 CGI 或`mod_perl`实时生成每个页面，但后来我决定每天生成一次内容，因为我的站点每天只更新一到两次。然而，正如你将在本节中了解到的，增加更新频率非常容易。`makepage`脚本假设每个页面由以下部分组成：

- 左侧导航栏
- 右侧导航栏
- 底部导航菜单
- 容纳页面内容的主体区域

每当在给定目录上运行`makepage`脚本时，它会查找所有以`.txt`扩展名结尾的文件，并创建相应的`.html`页面。例如，如果你在包含名为`index.txt`的文本文件的目录中运行`makepage`脚本，该脚本将运行并产生类似以下的输出：

## 使用 HTTP PUT 进行内网 Web 发布

脚本的输出显示它正在处理当前目录（用点字符表示）中的`index.txt`文件。然后它显示对于`index.html`使用的是哪个 RSB（右侧导航栏）模板文件。脚本首先查找名为`index-rsb.html`的 RSB 模板文件，如果找不到与该文本文件特定的 RSB 文件，它使用整个目录的默认 RSB 文件，碰巧是`default-rsb.html`。它对选择 LSB（左侧导航栏）模板重复相同的流程。然后它将当前的`index.html`（上次运行的输出）备份为`index.html.bak`，并使用默认正文模板`default-tmpl.html`来创建`index.html`页面。如果它找到名为`index-tmpl.html`的正文模板，它使用该模板而不是目录的默认正文模板。这使你在设计每个 Web 页面时具有灵活性。你可以简单创建一个目录范围的模板集，使目录中的所有页面看起来相同。或者你可以定制目录中的单个页面，拥有其自己的 RSB、LSB 和 BODY 模板。

如果你使用命令`makepage path_to_document_root`在文档根目录中运行该脚本，脚本会自动在文档根下的所有子目录中创建页面。因此，你可以将此脚本设置为`cron`任务，每小时、每天、每周甚至每分钟运行一次，具体取决于你的更新需求。内容作者只需放下他们的文本文件，页面就会自动创建。当放入新的文本文件时，如果你未提供页面特定的 RSB、LSB 或 BODY 模板，页面将使用目录的默认模板创建，这使得添加新页面极其简单。只需在你喜欢的文本编辑器中编辑一个页面，并通过 FTP 将该文件传输到你 Web 站点的正确目录，它应该会在下一次通过`cron`运行的`makepage`中发布。

随附光盘上提供的`makepage`包包含默认模板，你可以研究它们来构建自己的模板。

Apache 支持`PUT`方法，它允许你发布 Web 页面。然而，如果实施不谨慎，此功能会带来重大的安全风险。毕竟，你并不希望允许任何人更改你的 Web 站点。我只建议将此功能用于无法从 Internet 访问的内网。

你需要`mod_put`模块，它实现了 HTTP 1.1 中的`PUT`和`DELETE`方法。`PUT`方法允许你将内容上传到服务器，`DELETE`方法允许你从服务器删除资源。你可以从`http://hppwww.ec-lyon.fr/~vincent/apache/mod_put.html`下载此模块。

### 理解 `mod_put` 模块中的指令

`mod_put`模块提供三个指令来控制基于`PUT`和`DELETE`的发布。

#### `EnablePut`

`EnablePut`启用或禁用`PUT`方法。要使用`PUT`方法，你必须通过将此指令设置为`On`来启用它。

- **语法：** `EnablePut On|Off`
- **默认设置：** `EnablePut Off`
- **上下文：** `Directory`, `location`

#### `EnableDelete`

`EnableDelete On | Off`启用或禁用`DELETE`方法，该方法允许你通过 HTTP 删除 Web 页面。要使用`DELETE`方法，你必须通过将此指令设置为`On`来启用它。

- **语法：** `EnableDelete On | Off`
- **默认值：** `EnableDelete Off`
- **上下文：** `Directory`, `location`

#### `umask`

`umask octal_value`为目录设置默认的权限掩码（即`umask`）。`007`的默认值确保目录中的每个文件都以`770`权限创建，这仅允许文件所有者和组读取、写入和执行该文件。

- **语法：** `umask octal_value`
- **默认值：** `umask octal_007`
- **上下文：** `Directory`, `location`

### 编译和安装 `mod_put`

下载`mod_put`后，你需要执行以下步骤来编译和安装它：

1. 提取`mod_put.tar.gz`源文件，并将它创建的目录移动到 Apache 源发行版的`modules`子目录内。
2. 使用`configure`脚本（如果你之前已经编译过 Apache，则使用`config.status`）将`mod_put`模块添加到 Apache 中。使用`add --enable-module=put`选项运行任一脚本。
3. 使用`make && make install`命令编译和安装 Apache。
4. 使用`/usr/local/apache/bin/apachectl restart`命令重启 Apache。

### 设置启用 PUT 的 Web 目录

Netscape、AOLPress 和 Amaya 等 Web 客户端可以通过`PUT`方法发布 Web 页面。本节教你如何设置`httpd.conf`以在文档根树下的单个 Web 目录中启用基于`PUT`的发布。

> **警告**
>
> 如果你计划在内网之外使用`PUT`方法，请非常小心。在 Internet 上可访问的 Web 站点上使用`PUT`可能会极大地增加你的安全风险，因为如果这里描述的基于 Web 的身份验证过程被攻破，某人可以毁坏你的 Web 站点。我只建议将`PUT`方法用于内部使用。

1. 在`httpd.conf`中创建以下配置：

```text
Alias location_alias "physical_directory_under_document_root"

<Location location_alias>
    EnablePut On
    AuthType Basic
    AuthName "Name of the Web section"
    AuthUserFile path_to_user_password_file
    <Limit PUT>
        require valid-user
    </Limit>
</Location>
```
