
如果我们需要向仓库中添加内容，Subversion 提供了一个名为 `add` 的参数。如下例代码所示：

```
[[root@repo] svn add a new file to the repository]] -> add txt
[root@repo] svn add text
[root@repo] svn commit -m "Commit the fix"
```

注意，工作副本的目录包含一个名为 `.svn` 的特殊子文件夹。确保你不要删除或更改其中的任何内容，因为 Subversion 使用它来管理版本历史。

Subversion 带有许多功能，但在日常工作中我们只使用其中少数几个。这里我们使用其中几个来查看使用 Subversion 的典型工作流。

开发者使用 `status` 命令比任何其他 Subversion 命令都多。`svn status` 显示的最常见代码包括：

- `[?]` 项目文件或目录未被版本化

- `[M]` 项目已计划从 Subversion 仓库中删除

- `[A]` 项目已添加到 Subversion 仓库

- `[C]` 项目存在冲突。开发者需要在将更改提交到仓库之前解决冲突

1. 更新你的工作副本 - 使用 `svn update`

2. 对你的文件进行更改 - 编辑你想要更改的文件内容。例如，要移动和复制文件和目录，可以使用 Subversion 提供的 `svn add`、`delete` 和 `svn commit`

3. 审查更改 - 开发者可以使用 Subversion 的 `svn status` 和 `svn diff` 审查更改。

`svn` 命令还带有一个详细选项 `-v`，它会向你显示工作副本中项目的状态。

4. 修复错误 - Subversion 提供了 `revert`，这对于将文件或目录恢复到未修改的状态非常有用

`revert` 命令在许多场景下都非常方便。它可以恢复修改前的状态 - 如果你不小心从版本控制系统中删除了一个文件，可以使用它来恢复该文件

5. 解决冲突 - 这可以通过使用 `svn update` 和 `resolve status` 来完成。

Subversion 的另一个重要方面是解决冲突 - `svn update` 命令可以防止冲突。当你尝试将工作副本中的更改合并到仓库时，可能会发生冲突。当 Subversion 报告冲突时，它提供了一个开发者可以选择的选项，用于：

6. 发布更改 - `svn commit` 可用于将对仓库的更改传输到仓库，从而创建一个新版本以供使用。

选择：`p` 推迟，`d` 完整差异，`e` 编辑，`m` 我的-冲突，`t` 对方的-冲突，`s` 显示所有选项：

开发者将使用该选项，它会显示文件的所有修改以及任何冲突。到目前为止，我们已经了解了 Subversion 的基本方面。接下来，我们将更深入地研究此版本控制系统的高级功能。

www.linuxuser.com 51

## Qt 教程

## 在 Qt 中使用 HTTP 和 XML

Qt 提供了一个抽象层，保护你免受实现细节的影响

![](img/f32545dac69fddf8c1433ae8405b11b8_51_0.png)

CERN 的超文本传输协议 – HTTP 是现代 Web 的骨干。新闻源、网站和各种数据都可以通过这一悠久的协议获得。

Qt 的网络功能在诺基亚时代经历了一些动荡，一些著名的类被废弃，而另一些则被引入。这里我们使用 `QNetworkAccessManager` 类，它是 Qt 4 引入的，是访问资源的面向未来的方式。

Tom 从 Palm 时代就开始从事该行业了。作为一名记者、作者和科学家，他涵盖了 Tim Bern-Lee 团队最终创建的几乎基础性的协议用于传输标记的各个方面。随着他们的推移，创造了诞生现代 Web 的事物。HTTP 基于文本命令的交换。在大多数情况下，请求被发送到服务器，服务器用 HTML 数据进行响应。你可以轻松地设置创建由手动处理的请求。输入的数据可以使用 `QString` 的各种函数进行解析。

移动设备需要 Web 的灵活性，而 Qt 提供了许多预定义类，使得访问服务器变得轻而易举。包含 XML 可以节省许多时间，这些时间可以投入到更重要的任务中，例如应用程序的各个方面。检查文档可能是困难的，尤其是在非桌面操作系统上运行代码时。

RSS – 最初由哈佛创建。移动设备需要 Web 的灵活性，而 Qt 提供了大量的预定义类，使得访问服务器变得轻而易举。包含 XML 可以节省许多时间，这些时间可以投入到更重要的任务中，例如应用程序的各个方面。检查文档可能是困难的，尤其是在非桌面操作系统上运行代码时。

RSS – 最初由哈佛创建。移动设备需要 Web 的灵活性，而 Qt 提供了大量的预定义类，使得访问服务器变得轻而易举。包含 XML 可以节省许多时间，这些时间可以投入到更重要的任务中，例如应用程序的各个方面。检查文档可能是困难的，尤其是在非桌面操作系统上运行代码时。

## Qt 教程

至此，我们的请求开始在互联网上爬取。

传入的响应通过调用 `finished` 方法指示，该方法的起始如下：

```cpp
void QtFetcher::replyFinished(QNetworkReply* reply)
{
    QVariant redirection = reply->attribute(
        QNetworkRequest::RedirectionAttribute
););
    QUrl myRedirectedUrl = redirection.toUrl();
    if (!myRedirectedUrl.isEmpty()) {
        QtNetworkRequest request;
        request.setUrl(myRedirectedUrl);
        myManager->get(request);
    }
}
```

我们可以检查是否存在重定向。如果是此类情况，我们的代码将继续向新的目标地址发送另一个网络请求。

在示例中，虽然相对简单，但它仅限于检查 `URL` 是否与之前使用的 相同：

```cpp
QUrl QtFetcher::redirection(QUrl url, QUrl& possibleRedirection, QUrl oldUrl) {
    QUrl redirect1;
    if (!url.isEmpty() && possibleRedirection != oldUrl) {
        redirect1 = possibleRedirection;
    }
    return redirect1;
}
```

在处理重定向时，循环引用并不起见。这个问题可以通过限制重定向的次数来解决。如果你的应用被跳转了数十次，你可能会遇到麻烦。

一些开发者尝试构建一个链接的二叉树。然而，即使一个地址被访问了多次，服务器也可以通过创建由自动生成的 `URL` 网络重定向链来防止这一点。

## 接收传入的数据

大多数 Web 服务器以 HTML 格式交付数据，因此预期 XML 或 JSON 内容是合理的——在这里处理这些选择。

`QtNetworkReply` 提供了 `readAll` 方法，用于提取从服务器返回的文本内容。我们通过匹配内容类型来判断哪个格式是正确的。如果是 XML，我们将使用一个实例化并参数化的解析器类：

```cpp
void QtFetcher::replyFinished(QNetworkReply* reply)
{
    if (reply->readAll().isEmpty()) {
        return;
    }
    if (virtualParser->readNext().isStartElement()) {
        return;
    }
}
QXmlStreamReader item = virtualParser->readNext();
while (!item.isStartElement()) {
    if (item.name() == "item") {
        bool false=false;
        bool href=false;
        bool hasDescription=false;
        QString description, link, title;
```

这种过程通过多种方式进行处理；某些解析器可能会提供自动填充的注解类。在这里，我们的示例实现了一个简单的解析器，它将数据输出到状态机的馈送中，然后将其组装到各个存储器中。

-   注意无效输入

如果大多数馈送的格式不正确，就会出现奇怪的问题。当遇到此类标签时，映射你的。这是为了进行“模糊测试”：针对随机输入的特殊情况，然后提供给解析器。

> 大多数 Web 服务器是可信的。

正因如此，预期我们的方法能找到有用的内容是合理的

![](img/f32545dac69fddf8c1433ae8405b11b8_53_0.png)
