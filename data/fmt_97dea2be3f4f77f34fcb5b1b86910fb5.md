
请做好面对大量输出的心理准备。不要忽略它们；第一次阅读将帮助你理解 Docker 的工作原理。让我们将其拆分为与 Dockerfile 中的行对应的步骤。第一个任务是从 Docker 注册表获取最新版本的 Alpine 发行版容器：

```bash
Sending build context to Docker daemon 2.048kB
Step 1/3 FROM alpine:latest
Latest: Pulling from library/alpine
dcdbe7a58c2a: Complete
Digest: sha256-948b9263ad54c3d61834e29692c42d99f05c97c1ed7109ea4b954
Status: Downloaded newer image for alpine:latest
--->
```

注意这里对 SHA256 摘要和更短标识符的使用。习惯它们吧；Docker 需要跟踪许多小碎片。在这一步中，Docker 为 Alpine 发行版镜像创建了一个标识符为 `f7073ba266` 的新镜像。你之后可以引用那个特定的镜像，但可能不想这样做，因为它不是最终镜像。Docker 稍后会在此基础上构建更多内容。并非用于最终产品的镜像被称为**中间镜像**（intermediate image）。

使用 Podman 时输出会有所不同，但步骤是相同的。

我们配置的下部分是在 Alpine 中安装 bash shell 软件包。当你阅读以下内容时，你可能会认出 `apk add bash` 命令的输出结果（所示）：

```bash
Step 2/3 RUN add bash
---> 4f0fb4632b21
fetch http://dl-cdn.alpinelinux.org/alpine/v3.11/main/x86_64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/v3.11/community/x86_64/APKINDEX.tar.gz
(1/4) installing ncurses-base (6.1_p2020118-r4)
(2/4) installing ncurses-libs (6.1_p2020118-r4)
(3/4) installing readline (8.0.1-r0)
(4/4) installing bash (5.0.11-r1)
Executing bash-5.0.11-r1.post-install
Executing busybox-1.31.1-r9.trigger
OK: 8 MiB in 8 packages
Removing intermediate container 4f0fb4632b21
---> 12fe043c8c0a
```

在这个过程中某些并不显而易见。回想一下，你可能并没有在自己的机器上运行 Alpine。既然如此，你在这里运行属于 Alpine 的 `apk` 命令呢？

关键在于显示 `Running in 4f0fb462b31` 的那行。你还没有请求容器，但 Docker 已经使用上一步的中间 Alpine 镜像设置了一个新容器。容器具有标识符 ID；遗憾的是，它们看起来和镜像没有区别。为了避免混淆，Docker 将临时容器称为**中间容器**（intermediate container），这与中间镜像有所不同。中间镜像会保留一会儿；而中间容器不会。

在设置好 ID 为 `4f0fb462b31` 的（临时）容器后，Docker 在容器内部运行 `apk` 命令进行安装，然后并将更改保存到文件系统中，生成 ID 为 `12ef404c8a0` 的新中间镜像。注意，Docker 在完成后也会删除容器。

最后，当从新镜像启动容器时，Docker 执行运行 bash shell 所需的更改：

```bash
Step 3 : CMD "/bin/bash"
--> Running in fb082e6a0728
Removing intermediate container fb082e6a0728
--> 1b64f94e5a54
Successfully built 1b64f94e5a54
Successfully tagged hlw_test:latest
```

Dockerfile 中任何带有 `RUN` 命令的操作都发生在镜像构建期间，而不是在你用该镜像启动容器之后。`CMD` 命令是用于容器运行时；这就是为什么它发生在最后。

在这个示例中，你现在拥有一个 ID 为 `1b64f94e5a54` 的最终镜像，但因为你对它打了标记（通过两个独立的步骤），你也可以将其引用为 `hlw_test` 或 `hlw_test:latest`。运行 `docker images` 来验证你的镜像和 Alpine 镜像是否存在：

| docker images | TAG | IMAGE ID | CREATED | SIZE |
| :--- | :--- | :--- | :--- | :--- |
| hlw_test | latest | 1b64f94e5a54 | 1 minute ago | 9.19MB |
| alpine | latest | f70734b6266 | 3 weeks ago | 5.61MB |

## 运行 Docker 容器

你现在已经准备好启动容器了。在容器中运行某些有两种方法：

```bash
$ docker run -it hlw_test /bin/bash
```

这以带有 TTY 的交互模式启动容器。`-i` 标志表示交互式（interactive），`-t` 标志表示 TTY。这允许你与容器内部的 bash shell 进行交互。当你退出 shell（通过输入 `exit` 或按下 `Ctrl+D`）时，容器会停止。

如果你想在后台运行容器，请使用 `-d` 标志（分离模式，detached mode）：

```bash
$ docker run -d hlw_test
```

这会在后台启动容器，你可以使用 `docker ps` 查看其状态。要与运行的分离容器进行交互，请使用 `docker exec`：

```bash
$ docker exec -it <container_id> /bin/bash
```

这允许你在已经在运行的容器中打开一个新的 shell，而无需停止它。

宿主机。这可能会引起困惑，因为不同命名空间中的不同接口可能有相同的名称（例如，容器的 beeth0 以及宿主机的 beeth0）。

由于这使用了私有网络（而且网络管理员可能不想盲目地将任何内容路由到容器中），如果保持原样，使用命名空间的容器进程将无法访问外部世界。为了能够访问外部宿主机，宿主机上的 Docker 网络会配置 NAT。

图 17-1 显示了一个典型的设置。它包含了带有接口的物理层，以及 Docker 子网的互联网层，以及将该子网连接到宿主机其他部分及其外部连接的 NAT。

![](img/b73aaecfc9bbae176400133c41abe3c2_435_0.png)

图 17-1：Docker 中的桥接网络。粗线连接表示虚拟接口对的绑定。

> 注意：你可能需要检查你的 Docker 接口网络的子网。有时，它与电信公司路由器硬件分配的基于 NAT 的网络之间发生冲突。

Podman 中的无根（Rootless）操作网络是不同的，因为设置虚拟接口需要超级用户权限。Podman 仍然使用新技术，但它需要一个可以在用户空间运行的接口。这是一个 TAP 接口（通常是 tap0），并结合一个名为 slip-nets 的转发守护进程，容器进程就可以到达外部世界。这种能力较弱；例如，容器之间无法相互连接。

关于网络还有很多其他内容，包括如何在容器的网络栈中暴露端口以供外部服务使用，但网络拓扑是最重要理解的内容。

## Docker 操作

到这里，我们可以继续讨论 Docker 启用的其他类型的隔离和限制，但这将花费很长时间，而且你现在可能已经明白了要点。容器并不是源于某一个特定的特性，而是特性的集合。结果是，Docker 必须跟踪我们在创建容器时所做的所有事情，并且必须能够清理它们。

只要容器有进程在运行，Docker 就将其定义为“运行”状态。你可以通过 `docker ps` 显示当前运行的容器：

### docker ps

| CONTAINER ID | IMAGE | COMMAND | CREATED | STATUS | PORTS | NAMES |
|---|---|---|---|---|---|---|
| b6da624cef7 | hlw_test | /bin/bash | 8 hours ago | Up 8 hours | | boring_lovelace |
| 8a4d66e85fe | hlw_test | /bin/bash | 20 hours ago | Up 20 hours | | awesome_elion |

一旦所有进程终止，Docker 就会将它们放入退出状态，但仍保留容器（除非你使用 --rm 选项）。这包含了对文件系统所做的更改。你可以通过 `docker export` 轻松访问文件系统。

你需要意识到这一点，因为 docker 默认不显示容器；你必须使用 -a 来查看所有内容。积累大量容器非常容易，如果运行在容器中的应用程序创建了大量数据，你可能会耗尽磁盘空间却不知道为什么。使用 `docker rm` 来删除已终止的容器。

这也适用于旧镜像。开发镜像往往是一个重复的过程，当你用与现有镜像相同的标签为镜像进行标记时，Docker 不会移除原始镜像。旧镜像将丢失该标签。如果你运行 `docker images` 显示系统上的所有镜像，你可以看到它们所有的。这里有一个显示镜像之前的版本的示例：

### docker images

| TAG | IMAGE ID | CREATED | SIZE |
|---|---|---|---|
| hlw_test | b664f9e5a54 | 43 hours ago | 9.19MB |
| <none> | d0a61f5b379 | 46 hours ago | 9.19MB |
| alpine | f7073b4c6a266 | 4 weeks ago | 5.61MB |

使用 `docker rm` 来移除镜像。这会移除镜像构建产生的任何必要的中间镜像。如果你不移除镜像，它们会随着时间的推移而积累。取决于镜像以及如何构建，这可能会消耗系统上大量的存储空间。

通常，Docker 执行了许多细致的版本控制和检查点。这种管理层与 LXC 等工具（你很快就会看到）相比反映了一种特定的哲学。

## Docker 服务进程模型

Docker 容器的一个可能令人困惑的方面是内部进程的生命周期。在进程完全终止之前，由于镜像配置的方式很多，这可能会让你认为你不应该在 Docker 容器内部运行多个进程或服务。这是错误的。

你可以在容器中运行多个进程，但每个容器运行一个进程通常更好。这使得管理和扩展你的容器变得更容易。如果你需要运行多个进程，可以使用像 supervisord 或 systemd 这样的进程管理器。

在容器中运行多个进程的最佳方法是使用能够为你处理进程的进程管理器。这确保了如果其中一个进程崩溃，它将自动重启。

在容器中运行多个进程的另一种方法是使用启动所有进程的 shell 脚本。如果你希望进程使用本地端口相互通信，这可能很有用。然而，这种方法更难以管理和扩展。

# Linux 如何工作（早期访问版） - Brian Ward

这可以采取多种形式存在。如果你选择管理自己的基础设施，那是一项大量的时间投入，而且仍然有硬件和维护成本。如果你选择使用像 Kubernetes 集群这样的容器服务，那么你支付的是金钱成本，让别人替你完成工作。

在考虑容器本身时，请记住以下几点：

- 容器在存储方面可能是浪费的。为了让容器内的任何应用程序功能运行，容器必须包含 Linux 操作系统所需的所有支持，例如共享库。这会导致容器变得非常大，尤其是当你没有特别注意为容器选择的基础发行版时。再考虑你的应用程序本身：它有多大？当你使用带有多个相同容器副本的**叠加文件系统（overlay filesystem）**时，这种情况会得到缓解，因为它们共享相同的基础文件。然而，如果你的应用程序创建了运行时数据，这些叠加文件系统的上层可能会增长。
- 你仍然需要考虑其他系统资源，例如 CPU 时间。你可以设定容器消耗数量的限制，但你仍然受限于底层系统的处理能力。这涉及到时间内核和块设备。如果你过度存储或运行你的容器，底层系统或两者都会受到影响。
- 你可能需要以不同的方式思考数据存储位置。在 Docker 等使用叠加文件系统的容器系统中，运行期间对文件系统所做的更改在进程终止后就会被丢弃。在许多应用程序中，所有用户数据都会进入数据库，那么问题就简化为了数据库管理。但你的日志呢？这些日志对于运行良好的服务器应用程序是必须的，你仍然需要一种存储它们的方法。对于任何大规模的生产环境，独立的日志服务是必不可少的。
- 大多数容器工具和操作模型都是面向 Web 服务器的。如果你运行一个典型的 Web 服务器，你会在 Kubernetes 中找到大量关于运行运行 Web 服务器的支持和信息。特别是，它有许多防止服务器代码失控的安全功能。这可能是一个优势，因为补偿了大多数 Web 应用程序（坦率地说）写得相当糟糕的缺陷。然而，当你尝试运行其他类型的服务时，有时会感觉就像在试图把一个方木钉钉入圆孔。
- 粗率的容器可能会导致膨肿、配置问题和故障。你正在创建一个隔离环境这一事实，并不意味着你不会在该环境中犯错。你可能不需要过于担心系统的复杂性，但许多其他问题仍然会发生。当任何系统出现问题时，缺乏经验的用户倾向于通过添加内容来试图解决问题，而且通常是随意的。这可能会一直持续（通常是盲目地），直到出现一个功能尚存的系统——但伴随着许多额外的问题。你需要理解你所做的出的更改。
- 版本控制可能会出现问题。我们在书中的示例中使用了最新的（稳定）发布版本。这本应该是用于构建容器的最新版本，但也意味着当你基于发行版或包的最新版本构建容器时，底层的某些东西发生了变化并破坏了你的应用程序。一种标准做法是使用特定版本的基础容器。
- 信任可能是一个问题。这对于使用 Docker 构建的镜像尤为适用。当你以 Docker 仓库中的镜像为基础构建你的容器时，你实际上是在信任一个额外的管理层，信任它们没有被篡改以引入比比常更多的安全问题，并且在你需要它们时它们会在那里。这与 LXC 形成了对比，在 LXC 中，你会鼓励在某种程度上构建自己的镜像。

在考虑这些问题时，你可能会认为与其他管理系统相比，容器有许多缺点。然而，事实并非如此。无论你选择哪种方法，这些问题都会以某种程度和形式存在——而且其中一些问题在容器中更容易管理。记住，容器并不能解决所有问题。例如，如果你的应用程序在系统上启动需要很长时间，它在容器中也会启动缓慢。

## 17.3 运行时虚拟化

最后要提到的一种虚拟化是基于开发应用程序的环境类型。这与我们之前看到的系统虚拟机和容器不同，因为它并不使用将应用程序放在不同机器上的概念。它适用于特定的应用程序。

这些环境的原因是同一个系统上的多个应用程序可以使用相同的编程语言，导致潜在冲突。例如，Python 在典型发行版的许多地方被使用，并包含许多插件。如果你想在你的包中使用不同于系统的 Python 版本，可能会遇到麻烦。

让我们看看 Python 的虚拟环境功能如何创建一个只包含所需包的 Python 版本。开始的方法是这样创建一个环境目录：

```bash
$ python3 -m venv test-venv
```

> 当你读到这里时，你可能只需要输入 python 而不是 python3。

现在，查看新的 test-venv 目录。你会看到许多类似于系统的目录，如 bin、include 和 lib。要激活虚拟环境，你需要源（而不是执行）test-venv/bin/activate 脚本：

```bash
source test-venv/bin/activate
```

源激活的原因本质上是设置环境变量，而你无法通过执行来实现这一点。此时，当你运行 Python 时，使用的是 test-venv/bin 目录中的版本（它本身只是一个符号链接），并且 VIRTUAL_ENV 环境变量被设置为环境目录。你可以运行 deactivate 来退出虚拟环境。

这并没有那么复杂。在设置了这个环境变量后，你会在 test-venv/lib 中获得一个全新的空包库，任何新安装的包都会进入那里，而不是主系统的库。

并不是所有的编程语言都像 Python 那样允许虚拟环境，但值得了解它，至少可以消除对“虚拟（virtual）”一词的误解。

《逻辑是如何运作的早期访问版）2021，Brian Ward 著

Christensen, Tom, brian d foy, Larry Wall, and Jon Orwant, 《编程：处理与脚本的无与伦比的力量》，第4版. Sebastopol, CA: O'Reilly, 2012.

chromatic, 《现代 Perl》，第4版.Hillsboro, OR: Onyx Neon Press, 2016.

Davies, Joshua. 《使用密码学和 PKI 实现 SSL/TLS》。Hoboken, NJ: Wiley, 2011.

Friedl, Jeffrey E. F., 《精通正则表达式》，第3版. Sebastopol, CA: O'Reilly, 2006.

Gregg, Brandon, 《系统性能：企业与云端》，第2版. Boston: Addison-Wesley, 2020.

Grune, Dick, Kees van Reeuwijk, Henri E. Bal, Criel J. H. Jacobs, and Koen Langendoene, 《现代编译器设计》，第2版. New York: Springer, 2012.

Hopcroft, John E., Rajeev Motwani, and Jeffrey D. Ullman, 《自动机理论、语言与计算》，第3版. Upper Saddle River, NJ: Prentice Hall, 2006.
