
### 工作原理

正如我们所见，`systemctl` 工具可以用于完全控制你的系统服务。`systemctl` 是 `systemd` 的控制程序，而 `systemd` 是 CentOS 7 Linux 中的系统和服务管理器。`systemctl` 可用于各种任务，但此处我们专注于管理服务。

所以，我们从这次体验中学习了什么？

我们开始这个配方时登录 root 并安装了 Apache Web 服务器软件包，因为我们想用它来展示如何使用 `systemctl` 程序泛泛地管理服务。Apache 或被 systemd 称为的 `httpd.service` 只是我们将用作的一个示例；其他可能在基础服务器环境中运行的其他重要服务可能是 `ssh.service`、`mariadb.service`、`crond.service` 等。之后，我们通过 `systemctl status` 参数检查了 httpd 的当前状态。输出向我们展示两个字段：Loaded（已加载）和 Active（激活）。`Loaded` 字段告诉我们它是否已加载以及是否会在启动时自动启动；`Active` 字段表示服务当前是否正在运行。接下来，我们展示了如何使用 `systemctl` 启动服务。

> 通过启动服务时，程序会脱离终端并派生后台进程，这有时被称为守护进程。启动服务的精确语法是 `systemctl start <服务名称>`。

![](img/a6dbf7df749be83c0faae2334e970c0b_498_0.png)

## 管理系统

接下来，在我们启动 Apache 服务后，再次使用 `systemctl status` 参数查看状态。输出显示它已加载但已禁用（disabled）。我们通过该服务的最新输出看到它处于运行状态。要获取系统中所有服务的状态概述，使用 `systemctl --type service --all`。`systemctl` 服务不需要一直运行。它的状态可以是停止、降级等。我们使用以下命令列出系统的所有服务：

```
systemctl -t service -a
```

正如你所示，我们使用 `-t` 标志来过滤服务单元。正如你可能猜到的，`systemctl` 不仅可以处理服务单元，还可以处理许多其他单元。这些单元由 systemd 使用配置文件管理，这些封装了关于监听套字、保存的系统状态、挂载设备与其他对象的信息。要获取所有可能的单元的列表，输入 `systemd-help`。这些配置单元位于系统的特殊文件夹中，单元类型可以从系统中读取；所有扩展名为 `.service` 的服务单元（例如扩展名为 `.device` 的单元文件），系统有两个地方存储它们。所有系统单元都是通过安装软件包安装的。我们的 Apache 服务配置文件精确位于 `/etc/systemd/system/httpd.service`。我们向用户展示了如何启动服务（这是停止它的相反），语法为 `systemctl start <服务名称>`。最后，作为最后一步，我们使用了 `systemctl` 的 `restart` 参数，它处理服务的停止和启动，你可能需要重置它使其工作。

现在，想象你的 Web 服务器可以从互联网访问，并且此时有许多人正在并行访问你的网页或应用程序。如果你正常重启 Apache，Web 服务器将有一段时间无法访问（具体取决于重启服务器所需的时间），因为进程实际上会结束，然后重新从头开始。如果所有当前用户在这一刻正在请求某些内容，他们可能会收到 HTML 404 错误页面。此外，当前的会话信息也将丢失；想象你有一个在线商店，人们在那里使用购物车，这些信息也会消失。为了避免像 Apache Web 服务器这样重要服务的受到中断，其中一些服务提供了 `reload`（重载）选项（但并不是每个服务都有此功能！），我们可以用它来代替 `restart` 参数。服务将保持在线，并且在执行期间不会被中断。对于 Apache，你可以使用以下命令：`systemctl reload httpd.service`。要获取所有具有重载服务的列表，请使用以下命令：

```
grep -l *ExecReload* /usr/lib/systemd/system/*.service /etc/systemd/system.*
```

所以，有了这个配方，我们现在知道如何使用基本的 `systemctl` 参数来管理服务了。它可以是一个非常强大的程序，其用途远不止启动和停止服务这些。此外，在这个配方中，我们使用了不同的名称，但它们的意思相同：系统服务（system service）、后台进程（background process）或守护进程（daemon）。

### 更多

还有另一种单元类型称为 `target`（目标）。Targets 也是单元文件，你的系统中已经有很多这样的文件了。要显示它们，请使用以下命令：

```
ls -a /usr/lib/systemd/system/*.target /etc/systemd/system/*.target
```

简单来说，targets 是单元文件（如服务或其他目标）的集合。它们可以用于创建类似于运行级别（runlevel）的环境，你可能在早期的 CentOS 版本中见过它们。运行级别定义了在何种系统状态下加载哪些服务。例如，有图形状态、救援模式状态等。要查看常见的运行级别如何与我们的 target 对应，运行以下命令，它向我们显示所有的符号链接

```
ls -al /lib/systemd/system | grep runlevel
```

Targets 可以依赖于其他 target；为了获得 target 依赖关系的良好概览，我们可以运行以下命令来显示从多用户目标（multi-user target）到所有其他目标的依赖关系（绿色表示活动，红色表示未活动）：

```
systemctl list-dependencies multi-user.target
```

## 管理系统

你可以通过以下命令显示我们目前所在的 target：

```
systemctl get-default
```

你也可以切换到另一个 target：

```
systemctl set-default multi-user.target
```

## 排除后台服务的故障

通常，系统管理员工作的很大一部分是在出现问题时对服务器进行故障排除。这对于你的系统服务来说尤其如此，因为它们一直在运行并处理信息。服务可能依赖于其他服务以及服务器，在你的管理员生涯中，总会遇到系统服务失败或拒绝启动的情况。在这个配方中，我们将向你展示如果出现问题该如何进行故障排除。

### 准备工作

完成这个配方，你需要一个可以运行的 CentOS 7 操作系统安装、拥有 root 权限，以及你任选的控制台文本编辑器；你还应该已经完成了本章中的“了解和管理你的后台服务”配方，我们在那里安装了 Apache Web 服务器。

### 如何操作

为了展示如何排除服务的故障，我们将在 Apache 服务的配置文件中引入一个随机错误，然后向你展示如何排查并修复它：

1. 以 root 身份登录并输入以下命令向 `httpd.conf` 追加内容：
   `echo "THIS_IS_AN_ERRORLINE" >> /etc/httpd/conf/httpd.conf`
2. 接下来，重载 httpd 服务并显示其输出：
   `systemctl reload httpd.service`
   `systemctl status httpd.service -l`
3. 撤销这个错误：
   `sed -i '/s/THIS_IS_AN_ERRORLINE//g' /etc/httpd/conf/httpd.conf`
4. 现在，再次重启服务：
   `systemctl reload httpd.service`
   `systemctl status httpd.service`

### 工作原理

在这个短的示例中，我们展示了如果示例服务包含错误时会表现如何，以及你可以做什么来修复它以便入门。当服务发生故障时，有很多不同的场景会出现问题，解决这类问题可能是系统管理员工作的很大一部分。

所以，我们从这次经历中学习到了什么？

我们开始这个配方时，在 Apache 主配置文件引入了一行文本，该文本不包含任何有效的配置语法，因此 http 服务无法解析它。然后，我们使用 `systemctl reload` 参数来重载服务器的配置文件。如前所述，并不是所有服务都有 `reload` 选项，所以如果你感兴趣的服务不支持它，请改用 `restart` 参数。由于 Apache 将尝试使用我们当前的更改来重载配置，由于语法错误，它将拒绝接受新配置。由于我们是在重载配置，运行中的 Apache 进程不会受到此问题的影响，并将使用其原始配置保持在线。`systemctl` 参数将打印以下错误消息，为我们下一步的操作提供提示：

```
Job for service.failed. Take a look at systemctl status http.service.
```
