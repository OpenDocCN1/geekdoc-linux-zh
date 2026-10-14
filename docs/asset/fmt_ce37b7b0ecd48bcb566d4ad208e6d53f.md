
```
matthewapp@seymour:-$ apt-cache showsrc python-vigra | grep ^Package:
Package: libraigimpex
```

在第一个示例中，`tomboy` 在 `tomboy` 软件包中。在第二个示例中，二进制 `python-vigra` 在 `libraigimpex` 软件包中。当你知道包含所需源码的软件包后，获取源代码本身的副本。在 Ubuntu 中，你通过对源包进行分支（branching）来实现这一点。Launchpad 管理所有源包的代码，它是你下载并创建本地分支的地方。你在本地分支中修复 bug 并在机器上测试它们，然后提交一个合并提案（merge proposal），以便你分支中的代码可以被检查并合并回代码的主分支，用于构建该代码的新软件包。

在你的机器上为代码创建一个本地存储库，再次将 `matthewapp` 替换为你所需的源包名称：

```
matthewapp@seymour:-$ bzr init-repo matthewapp
```

切换到新创建的目录：

```
matthewapp@seymour:-$ cd matthewapp
```

创建一个本地分支并给它起一个显目易懂的名字。许多 Ubuntu 开发者会将新的目标目录命名为与原始相同，并在末尾添加 `.dev`，如下：

```
matthewapp@seymour:-$ bzr branch ubuntu:matthewapp matthewapp.dev
```

在你对 Ubuntu 存储库中已有的软件包完成几次操作后，你可以阅读官方的《Ubuntu 打包指南》，了解如何对来自其他 Ubuntu 版本、Debian 或上游 `.tar` 代码执行类似任务。本节侧重于通过这种简单的方法来帮助你入门。

创建一个包含 bug 修复的补丁：

```
mathew@seymour:-$ edit-patch 99-new-patch
```

这会将文件的打包拷贝到一个新的临时目录。使用文本编辑器编辑文件，或在临时 shell 中使用补丁完成，如下：

```
mathew@seymour:-$ patch -pl ../bugfix.patch
```

你可以通过输入 `exit` 或使用 `Ctrl+D` 退出临时环境。

使用你的补丁构建测试包以测试你的更改，将 `release` 替换为发布名称（例如 `quantal`），并将 `package` 和 `version` 替换为软件包编号：

```
mathew@seymour:-$ dbuild -scc quantal
```

如果构建成功，在本地安装测试包以查看其运行情况：

```
mathew@seymour:-$ dpkg -i ../build/package_version.deb
```

当你对更改满意时，创建一个更改日志条目：

```
mathew@seymour:-$ dch
```

最后，将你的更改推送到 Launchpad：

```
mathew@seymour:-$ bzr push lp:yourLaunchpadID/ubuntu/release/branchname
```

## 参考文献

- https://uds.ubuntu.com — Ubuntu 开发者峰会主网站
- http://developer.ubuntu.com — Ubuntu 开发主网站
- http://developer.ubuntu.com/apps — 开发运行在多个设备平台上的 Ubuntu 应用程序的有用资源，包括 Ubuntu SDK
- https://myapps.developer.ubuntu.com/dev/ — 用于创建 Ubuntu 程序的额外资源集
- http://developer.ubuntu.com/resources/ — Ubuntu 开发有用资源的优秀列表
- http://packaging.ubuntu.com — Ubuntu 打包指南主网站
- http://harvest.ubuntu.com — Harvest 的主网站
- https://wiki.ubuntu.com/UbuntuDevelopment/BugFixingInitiative — Ubuntu 社区 Bug 修复计划主网站
- https://wiki.ubuntu.com/MOTU — Ubuntu 社区“宇宙大师”团队主网站
- http://daniel.holba.ch/blog/ — Daniel Holbach 的博客

# 第 43 章

### 本章内容

# 协助 Ubuntu 测试与质量保证（QA）

- 社区团队
- Bug 小组（Bug Squad）
- 参考文献

有很多方法可以帮助 Ubuntu 社区创建、完善和推广该操作系统。有些具有很高的技术性，例如编写代码或打包程序以包含在软件仓库中。有些技术性较低，例如在本地帮助 Ubuntu，或者通过博客分享社区的趣闻新闻。在中间位置，偏向技术的一侧，有一项任务非常开放，欢迎更多社区的参与。

这是一个相当简短且刻意模糊的章节。志愿者所的测试如果想要对开发者有帮助而不是成为困扰，需要的不仅仅是业余的兴趣。因此，本章涵盖了如何参与的基础知识和一些机会，但没有提供精确的细节。如果你感兴趣——在读完本章后，我们希望你是感兴趣的——下一步是访问章节末尾“参考文献”部分中的网站。

## 社区团队

两个团队——Ubuntu 测试团队和 Ubuntu QA 团队——非常欢迎能够遵循指示、细心且有方法、并留意细节的志愿者。两个团队都希望在开发周期内完善发行版，使 Ubuntu 尽可能完美。

Ubuntu QA 团队直接关注发行版的整体质量，尝试默认配置文件和配置，并尝试让系统崩溃。目标是在开发周期内发现 bug 并对它们提交清晰的报告，以便在终端用户知道它们存在之前将其修复。这里的目标是产品改进和质量控制或保证。

这些都是巨大的任务。即使有几位 Canonical 员工全职工作，几乎不可能测试每种硬件配置或用例。无法猜测用户会以何种方式执行开发者设计为不同方式执行的任务。当目标是为尽可能多的人创造积极体验时，尽可能测试这些选项之一是关键。这就是为什么志愿者既是活跃的，又在不断招募。

这些也是严苛的任务。测试和 bug 报告需要仔细的关注，以确保报告的问题清晰，并附有开发者可以重复的步骤。这使他们能够找到问题所在并更轻松地修复它们。每个人都适合这类事情，但那些能够清晰、精确并遵循测试计划和程序指示的人是价值连城的。你可能不会因为测试获得公开声誉，但如果你能把工作做好，将获得与你一起测试的同事的荣誉。

你会注意到在这些团队的任务描述中存在一些交叉，说明它们工作得非常紧密。每个团队都有一个主重点，两个团队不时执行相似的任务。甚至个人的个人网页也相互链接并提供类似的信息。
