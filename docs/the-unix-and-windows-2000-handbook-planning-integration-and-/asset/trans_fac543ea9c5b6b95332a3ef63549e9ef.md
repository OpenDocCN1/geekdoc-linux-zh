
手册页的新增内容将立即对用户可用，用户无需执行任何操作。

例如，假设你的用户要求你在系统上安装程序 foo。你发现 fooware 的最新版本是 3.5。你应该创建目录 /usr/local/lib/fooware.3.5，并在其中安装和编译 foo 3.5 版本。完成后，在 /usr/local 中创建一组符号链接，使用：

```
#mkdir /usr/local/lib/fooware.3.5
#ln -s /usr/local/lib/fooware.3.5 /usr/local/lib/fooware
#<install fooware 3.5 software>
#ln -s /usr/local/lib/fooware.3.5/bin/foo /usr/local/bin/foo
#<install manual pages>
```

最后，将手册页安装在 /usr/local/man 中。

通常，就在你告诉用户 foo 3.5 版本可用之后不久，fooware 3.6 版本就发布了。当你下载最新版 fooware 时，应该创建目录 /usr/local/lib/fooware.3.6。然后在你测试完 foo 3.6 版本后，要使 foo 3.6 成为受支持版本，只需按如下方式更改 /usr/local/lib 中的链接：

```
#mkdir /usr/local/lib/fooware.3.6
#<install fooware 3.6 software>
#rm /usr/local/lib/fooware
#ln -s /usr/local/lib/fooware.3.6 /usr/local/lib/fooware
#<install manual pages>
```

- /usr/local/bin 中的符号链接无需修改，你的用户不会察觉到任何差异。

如果你选择做一位仁慈的管理员，可以通过在 /usr/local/bin 中创建如下符号链接，让用户轻松访问 fooware 3.5 版本：

```
#ln -s /usr/local/lib/fooware.3.5/bin/foo /usr/local/bin/foo-3.5
```

这是一种继续支持旧软件版本的简单方法，且不会影响大多数用户群体。

## 设计单一供应商的 /usr/local 基础设施

你选择安装在 /usr/local 中的应用程序数量将直接影响你管理 /usr/local 仓库所花费的时间。虽然管理单个系统上的 /usr/local 对管理员来说可能是一项全职工作，但如果你拥有一个由许多系统组成的分布式基础设施，且所有系统都需要访问 /usr/local，会发生什么？

在每个系统上都安装每个新软件包，既不是对你时间的好利用，也不是对系统资源的好利用。通过使用 NFS 进行文件共享以及软件分发技术，你需要开发一个 /usr/local 基础设施来满足用户的需求。

设计你的 /usr/local 基础设施应遵循与设计 DNS 和 NIS 基础设施相同的逻辑，只需稍作修改。

在制定 /usr/local 策略时，应牢记以下四个关键要素：

- 确定一台中心机器作为主 /usr/local 服务器，并且仅在该系统上安装所有新软件包，以保持一致性。
- 确定整个基础设施中可以充当额外 /usr/local 服务器的其他系统。服务 /usr/local 的文件服务器资源与服务 DNS 或 NIS 的资源不同。充当文件服务器会增加服务器的处理和 I/O 负载，并消耗磁盘资源来维护一份 /usr/local 副本。
- 在拥有大量用户的大型分时系统上，如果有可用资源，请在本地磁盘上保留一份 /usr/local 的副本。通过网络从 NFS 挂载的 /usr/local 运行程序会增加网络流量，并影响本地系统用户性能。
- 每晚复制 /usr/local 文件以确保文件保持同步。当你对主 /usr/local 服务器进行更改时，请确保建立一个流程，使所有 /usr/local 副本保持一致。这有助于为你的用户提供稳定的环境，他们会为此感谢你。

确定一个中心系统作为你的主仓库非常重要。你将在这个系统上执行所有安装和测试。如果可能的话，请选择一个没有用户或用户数量最少的系统。在用户尝试工作时更改符号链接，并不是让用户对你保持好感的最佳方式。此外，在选择额外的 /usr/local 服务器时，请确保它们拥有充足的资源，不仅能够处理当前的 /usr/local，还能应对未来的增长。

> 如果后来因为磁盘空间耗尽而不得不更换 /usr/local 服务器，这可能是一个痛苦的过程，尤其是当你有许多系统使用该 /usr/local 服务器，并且需要重新配置以指向另一台服务器时。
