

## 17.5.7.7 GitHub 作为远程仓库

GitHub 是一个流行的远程仓库，您可以在其中轻松、安全地与团队协作进行软件项目的开发和维护。我们首先提供有关 Git URL 和 refspec 的一些背景信息。然后，在本节的示例中，我们展示了如何使用 UNIX 命令行将文件从本地仓库传输到 GitHub 仓库的基础知识。我们还展示了如何从 GitHub 获取文件并将其检索回本地仓库。这些操作的基础和准备工作在 UNIX 命令行上通过我们迄今为止所展示的 Git 命令来加速。因此，完成前面关于 Git 的小节对于理解此处所示的 GitHub 交互是必要的。我们还引入了新的 Git 命令，以便您能够与 GitHub 远程仓库协作。

我们没有展示如何在 GitHub 上获取账户，或如何使用 GitHub 的基于 Web 的 GUI 界面创建新仓库。假设在所有示例中，您都可以通过 Web 浏览器在 www.github.com 上完成这两个基本步骤，并且可以导航到我们显示的 URL。您系统上的仓库称为本地或当前仓库，而像 GitHub 这样的仓库称为远程仓库。

使用 git remote 命令及其选项和参数来创建、删除、操作和查看远程仓库。例如，要向当前本地仓库添加远程引用规范，或 refspec，请使用 git remote add 命令及其选项和参数。您也可以查看 .git/config 文件中已定义为远程的内容。您添加的所有远程仓库都记录在 .git/config 文件中，可以使用 git config 及其选项和参数进行操作。

引用远程仓库的基本 Git 命令是

| git clone | 将远程仓库传输到本地仓库 |
| git fetch | 从远程仓库检索对象及其相关数据结构 |
| git pull | 将远程仓库中的更改合并到对应的本地分支 |
| git push | 将对象及其相关数据结构复制到远程仓库 |
| git ls-remote | 列出给定远程仓库中的引用 |

### 17.5.7.7.1 Git URL

对于 git remote 命令，Git 将对远程仓库的引用参数形式命名为统一资源定位符（URLs）。引用本地文件系统上仓库的 Git URL 可以是：

```
/pathname/repo.git
file:///pathname/repo.git
```

第一种引用形式使用 UNIX 文件系统中的硬链接，在当前和远程仓库之间直接共享完全相同的对象。第二种且首选的形式是复制数据而不是通过链接共享。

引用远程系统上仓库的 Git URL 可以采用多种形式。这些形式包括 http、https、ssh、scp、rsync 和 ftp。我们在示例中使用的主要且首选的通过 http 或 https 指定远程仓库的方式如下。

```
http://github.com/pathname/repository_name
https://github.com/pathname/repository_name
```

其中 pathname 是 GitHub 上的用户名，repository_name 是该用户的特定命名仓库。命名仓库不必以 .git 后缀结尾。这两种 URL 形式是 GitHub 最青睐的。

服务器防火墙通常允许 http 端口 80 和 https 端口 443 保持开放，并且在 PC-BSD 上默认情况下 ssh 的端口 22 也是开放的。

对于必须通过广域网（如互联网）检索数据的远程仓库，您还可以使用 Git 原生协议，该协议指的是 Git 内部用于传输数据所使用的自定义协议。原生协议 URL 的示例包括

```
git://example.com/pathname/repo.git
git://example.com/~user/pathname/repo.git
```

这些形式由 Git 用于匿名读取发布仓库。您可以使用这些 URL 形式进行 clone 和 fetch。

Git 原生协议可以通过 ssh 连接进行隧道传输，使用以下 URL 规范：

```
ssh://[user@]github.com[:port]/pathname/repo.git
```

其中 user@ 是本地系统上的客户端 ssh 用户名，port 是客户端上除默认端口 22 之外的可选端口指定，pathname 是 GitHub 上的用户名，repo.git 是 GitHub 上特定仓库的名称。

