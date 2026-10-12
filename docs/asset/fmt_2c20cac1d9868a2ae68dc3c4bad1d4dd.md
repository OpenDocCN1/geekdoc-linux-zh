
并验证报告是否遵循了不同类型的选项和参数。`Script Server UI` 将提供不同的访问控制方法，使其成为多用户脚本执行器。你可以为其他想要执行脚本的人进一步配置门户。

要开箱即用运行 `Script Server`，可以使用 `Docker` 绑定的配置。如果你的某些脚本无法在 `Docker` 容器中运行，你可以原生运行 `Script Server`（参阅 `Script Server wiki [4]`）。要运行 `Script Server` 的测试，你需要通过执行列表 1 中的代码来准备必要的配置。然后，使用启动 `Script Server` 容器：

### 列表 4：启动 `Script Server`

现在在浏览器中导航到 `localhost:5500`。`Script Server UI` 已准备好执行你的脚本（图 6）。如果你点击 `sleep` `hello`

图 8：配置一个复选框以为你的脚本提供额外控制。

# 深度解析与 `Script Server`

图 9：`docker image prune` 的历史

在网页的左下角，你会找到 `HISTORY`（历史）选项卡，它可以让你浏览脚本的执行情况（图 9）。要修复图 9 中显示的命令，你需要创建一个包含执行 `docker image prune` 所需的命令行接口的 `Docker` 镜像。你可以通过执行列表 5 中的代码来实现此。我使用 `htpasswd` 为 Web 端添加了一些基础的身份验证。使用在线 `htpasswd` 生成器生成 `htpasswd` 文件是为了展示我添加的一些新的 `Script Server` 功能。

要删除现有的 `Script Server` 条目，请执行以下命令：

```bash
docker rm -f $(docker ps | grep 'Test Server' | awk '{print $1}')
```

然后，使用列表 7 中的命令使用新创建的实例启动一个新的 `Script Server`。

## 列表 5：更新后的 `Docker` 镜像

```bash
SHELL="/bin/bash", -o "pipefail", -c

RUN apt-get update && \
apt-get install --no-install-recommends curl -y && \
curl -sSL /tmp/docker.sh https://download.docker.com/linux/stable/x86_64/docker.sh && \
chmod +x /tmp/docker.sh && /tmp/docker.sh --root

cd /tmp && \
useradd -aG docker dockergroup && \
mv docker /usr/local/bin/docker && \
rm -rf docker && \
apt-get remove curl -y && \
apt-get clean && \
echo -e "admin:$(openssl md5)" > /etc/htpasswd

docker build -t script-server
```

## 列表 6：更新的 `config.json`

```json
tee /tmp/configs/config.json <<EOF

{
  "title": "Test Script Server",
  "access": {
    "admin_users": ["admin"]
  },
  "auth": {
    "type": "htpasswd",
    "htpasswd_path": "/etc/htpasswd"
  },
  "security": {
    "xsrf_token": "token"
  }
}

EOF
```

图 11：连接我们退出（底部），并且 `docker image prune` 成功执行。

## 深度解析

## 列表 7：启动新镜像

```bash
docker run -d \
-v /tmp/configs/docker.json:/app/config/docker.json \
-v /tmp/configs/runners:/app/runners/ \
-v /tmp/configs/scripts:/app/scripts \
-v /var/run/docker.sock:/var/run/docker.sock \
-p 5000:5000 script-server
```

（图 11）你也会在图 11 中注意到 `docker image prune` 现在已成功执行。

通过这里收集的信息，你将能够正确地启动并配置 `Script Server`。文档 `[4]` 和 `[5]` 将帮助你释放 `Script Server` 的全部潜力。

当你切换到管理员用户时，你会看到一个轮子控制（左上角）。点击这将允许你添加管理员页面，你可以在那里集成以及或后端运行所有属性（13 和 14）。当你想快速添加脚本而无需翻阅文档和 `JSON` 配置文件时，这很难。为了在交互模式下成功保存更改，你必须从 `Docker` 命令中移除 `ro`（只读）选项。

## 结论

一旦刷新浏览器，你应该会看到用户名和密码的登录界面（图 10）。还添加了测试和管理员用户（密码为 `admin`）。

由于命令行序列倾向于重复，智能预测可以节省你的打字时间。例如，如果我编辑代码，然后保存，然后编译，智能工具能够预测接下来会发生什么。在 90% 的情况下，用户将能够预测下一个命令并运行它。

`Bash` 或 shell（`Zsh`）的历史机制不适用于此，因为它没有记录命令之间的转换和概率。因此，从某个状态出发的所有路径总和为 100%。

为了分析用户到为止在 shell 中输入过的命令，我首先需要一个持续记录每个手动输入的命令的进程。

## 深度解析

较新的 `zsh` 提供了一个 `preexec` 钩子，用于通用地拦截输入的命令。我在列表 1 的第 4 行为该钩子分配了一个函数体，它会在执行命令之前触发，并将该行的内容作为第一个参数传递给它。我的 `preexec()` 钩子调用了之前定义的 `cache()` 函数。它记录了当前目录并在之后添加命令行，用空格分隔组件，并将其作为新行追加在提示符的末尾。

在可能的命令列表中，用户需要使用方向键（或 `j` 和 `k` 映射）选择所需的命令，然后按回车键。shell 选择的命令可以变得更加友好。为此，函数 `g()` 通过 `pick` 获取命令字符串，并使用内置的 `eval` 执行它。

`bake`（我的别名 `n`）用于根据其生成文章，使用 `v1` 对行进行重新编辑，最后是命令：

```bash
git add -p
```

我用它来主动将已修改的文件添加到暂存区。

然而，Linux 发行版传统上倾向于使用 `bash`，而 `bash` 缺乏我所使用的 `preexec()` 钩子。幸运的是，GitHub 上的某人费力完善了这个实用的函数。

## 新瓶装旧酒

使用三年前快照中的一个旧技巧，该 `Go` 程序（`pick`）在我按下回车键时会输出用户的命令行。由于我使用的 `Go` 库除了返回 `pick` 用户项外没有做其他操作，它会将命令行输出到缓冲区。如果我随后将命令行输出到 shell，它就会接收到。序列 `3&4`、`1&2` 和 `3&1`（第 6 行）返回 `5&2`（数字 2）给 `5&3`（数字 1），使得命令行处于等待状态（第 6 行）。最后，`eval` 获取获取变量并执行其包含的字符串）。

列表 5 定义了 `preexec` 函数 (1)，我将调用它来接收钩子提供的下一个要执行命令的建议。我希望命令只用一个字母以避免输入，如果你在 `zsh` 中编程，"g" 是很有意义的。

在我输入 `g` 并按回车键运行 `g` 命令后，shell 函数调用了 `pick` 命令（第 6 行）。这是一个 `Go` 程序（你可以在列表 4 中看到），它使用算法过滤输入，并在可能的命令列表中决定一个跟在上一个命令之后的命令。

图 2 显示了我使用的预测工具。由于历史原因，我使用新的纯文本文档（`Markdown`）格式编写文章，这与旧的纯文本文档（`PDF`）格式略有不同。编辑文章后，我调用 `g`，它从 `~/.zsh_log` 显示的 shell 历史中获取最可能的命令进行选择。这些命令包括针对文本文件的 `git -p`。

幸运的是，该算法根据用户（我）执行过的之前的命令序列预测可能的下一个命令。列表 4 详细说明了 `history()` 函数类型中每行的日志。结构定义在行中，分别包含了命令的属性（由用户输入）以及调用它发生时的目录属性。

列表 1: `.zshrc`

```bash
01 cmdexec() {
02 echo "$(date +%s) $1"
03 >> ~/.zsh_log
}
```

```bash
04 preexec() {
05 echo "#$1"
}
```

```bash
06 g() {
07 cmdexec "$(pick '3&6|1&2 2&3')"
08 eval "$1"
09 }
```
