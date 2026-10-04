
# 在 Ubuntu 上安装 SQL Server 2017

你已经看过了使用 Red Hat Enterprise Linux 安装和配置 SQL Server 2017 的整个过程。现在，让我们在 Ubuntu 上安装 SQL Server。之后，我将只关注与之前的 Red Hat 安装相比不同之处。让我们从创建一个运行 Ubuntu 的虚拟机开始。

打开 Microsoft Azure 虚拟机门户。在搜索框中输入 Ubuntu。这会向你显示几个结果。选择 Ubuntu 16.04 LTS。每个 Linux 安装对于 SQL Server 2017 至少需要 3.25GB 内存，或者目前你位于画库中的虚拟机镜像至少有这么多内存，所以这应该不是问题。如果你使用其他方法创建虚拟机或自己手动安装操作系统，则需要小心。

按照本章前面“创建虚拟机”部分描述的步骤操作。一旦虚拟机运行且你能够连接到它，请运行语句获取公共存储库 GPG 密钥（稍后会详细介绍）：

```bash
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add key
```

接下来，运行以下语句来注册 SQL Server Ubuntu 仓库：

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list | sudo tee /etc/apt/sources.list.d/mssql-server.list
```

对于 Red Hat Enterprise Linux，这是累积更新仓库。GDR 仓库位于 `https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-grdr.list`，预览仓库位于 `https://packages.microsoft.com/config/ubuntu/16.04/mssql-server.list`。

最后，运行以下命令安装 SQL Server：

```bash
sudo apt-get update
sudo apt-get install -y mssql-server
```

## 配置 SQL Server

从此开始，你可以像以前一样通过运行以下命令来配置 SQL Server，接受许可条款，选择免费开发者版并提供一个强 `sa` 密码：

```bash
sudo /opt/mssql/bin/mssql-conf setup
```

你将看到类似下方的输出：

```text
此产品的许可条款可以从 http://go.microsoft.com/fwlink/?LinkId=746388 下载，并在 /usr/share/doc/mssql-server/LICENSE.TXT 中找到。

你是否接受许可条款？[是/否]:Yes

选择 SQL Server 版本：

- 1) 评估版（免费，无生产环境使用权，180 天限制）
- 2) 开发者版（免费，无生产环境使用权）
- 3) Express 版（免费）
- 4) Web 版（付费）
- 5) 标准版（付费）
- 6) 企业版（付费）
- 7) 我通过零售渠道购买了许可，并有密钥需要输入。

关于版本的详细信息可以在此处找到：https://www.microsoft.com/en-us/sql-server/sql-server-2016-editions

使用此软件的付费版本需要通过 Microsoft 批量许可计划单独获得许可。通过选择付费版本，你正在确认你有相应数量运行此软件的许可。

输入版本 (1-7): 2

输入 SQL Server 管理员密码：
确认 SQL Server 管理员密码：

正在配置 SQL Server...
这是一个评估版本。评估期还有 [170] 天。已创建从 /etc/systemd/system/multi-user.target.wants/mssql-server.service 到 /lib/systemd/system/mssql-server.service 的软链接。

设置成功完成。SQL Server 正在启动。
```

## 安装客户端工具

安装客户端工具也与 Red Hat Enterprise Linux 不同。请先导入公共存储库 GPG 密钥。

接下来，运行以下语句来注册 SQL Server Ubuntu 仓库：

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list | sudo tee /etc/apt/sources.list.d/mssql-server.list
```

最后，运行以下命令安装 SQL Server：

```bash
sudo apt-get update
sudo apt-get install -y mssql-server
```

从此开始，你可以像以前一样通过运行以下命令来配置 SQL Server，接受许可条款，选择免费开发者版并提供一个强 `sa` 密码：

```bash
sudo /opt/mssql/bin/mssql-conf setup
```

最后，如安装输出所示，请运行以下命令来配置 SQL Server 集成服务，再次选择 2 以选择免费开发者版：

```bash
sudo /opt/ssis/bin/ssis-conf setup
```

# 在 SUSE Linux Enterprise Server 上安装 SQL Server 2017

按照你之前的方法使用 `mssql-conf` 工具配置 SQL Server：

```bash
sudo /opt/mssql/bin/mssql-conf setup
```

最后，安装 SQL Server 客户端工具。使用以下步骤在 SUSE Linux Enterprise Server 上安装 `mssql-tools` 包。将 SQL Server 存储库添加到 `zypper` 中：

```bash
sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo
sudo zypper --gpg-auto-import-keys refresh
```

连同 `unixODBC-devel` 开发包安装 `mssql-tools`：

```bash
sudo zypper install mssql-tools unixODBC-devel
```

使用 `sqlcmd` 命令行工具照常连接：

```bash
/opt/mssql-tools/bin/sqlcmd -U sa
```

此时运行 `SELECT @@VERSION` 显示如下内容：

```text
Microsoft SQL Server 2017 (RTM-CU2) (KB405274) - 14.0.3008.27 (X64)
Nov 16 2017 10:00:49
Copyright (C) 2017 Microsoft Corporation
Developer Edition (64-bit) on Linux (SUSE Linux Enterprise Server 12 SP2)
```

按照之前指示的相同步骤从虚拟机外部连接。

你需要在网络安全组上配置入站规则，允许使用 TCP 端口 1433 的 SQL Server 客户端连接。

与 Red Hat Enterprise 和 Ubuntu 的操作一样，现在我将介绍如何在 SUSE Linux Enterprise Server 上安装 SQL Server Agent、SQL Server 全文搜索和 SQL Server 集成服务。要安装 SQL Server Agent，运行以下命令：

```bash
sudo zypper install mssql-server-agent
```

要安装 SQL Server 全文搜索，运行以下命令：

```bash
sudo zypper install mssql-server-fts
```

安装这些组件后，你需要重启 SQL Server：

```bash
sudo systemctl restart mssql-server
```

最后，截至本文编写，SQL Server Integration Services 尚未适用于 SUSE Linux Enterprise Server。

# 在 Docker 上运行 SQL Server

Docker 是一种软件技术，它提供容器作为额外的抽象和自动化层，用于我们非常熟悉的虚拟化技术。Docker 可以在 Linux、Windows 或 Mac OS 上运行。

在 Docker 上使用 SQL Server 与之前的 Linux 安装之间的根本区别在于，Docker 将运行一个预有的 SQL Server 2017 镜像。目前提供的镜像是 Ubuntu 16.04 上的 SQL Server 2017。请记住，此 Ubuntu SQL Server 2017 镜像可以在任何支持 Docker 容器的操作系统上运行。要在 Docker 上运行 SQL Server 2017，你首先需要安装 Docker。由于配置 Docker 的方法可能有，在本次练习中我将在 Ubuntu 虚拟机上演示 Docker。

例如，为了在我之前的 Ubuntu 虚拟机镜像上运行 Docker，我使用以下命令：

```bash
$ docker
```

我得到了如下响应：

```text
The program 'docker' is not installed. You can install it by typing:
sudo apt install docker.io
```

我遵循了建议并运行了以下命令：

```bash
sudo apt install docker.io
```

> **注意**：SQL Server 2017 在 Docker 上需要 3.25GB 的内存，请确保主机配置了至少 4GB 的内存。这是我在某些默认 Docker 安装中发现的一个常见问题。

接下来，我们需要通过运行以下命令下载 SQL Server 2017 镜像：

```bash
sudo docker pull microsoft/mssql-server-linux:2017-latest
```

以下是我安装时的部分输出：

```text
Using default tag: latest
latest: Pulling from microsoft/mssql-server-linux:2017-latest
aed5891ba52: Pull complete
773ae8583d14: Pull complete
d1d48771f72: Pull complete
cd3d6cd60cf: Pull complete
8ff6f8a9120c: Pull complete
1fd7e8b10447: Pull complete
bd48157db89: Pull complete
273a1970ce9c: Pull complete
fe20b2602177: Pull complete
086b9c4d6d68: Pull complete
Digest: sha256-38346f8eba690c997ff3b511188d1f3c0731a77784a25e3165eecc5f592a1498
Status: Downloaded image for microsoft/mssql-server-linux:2017-latest
```

接下来，我们准备好在 Docker 上运行 SQL Server 镜像，在执行下一个语句的同时指定合适的 `sa` 密码：

```bash
docker run -e 'ACCEPT_ULA=Y' -e 'MSSQL_SA_PASSWORD=password' -p 1421:1433 --name sqlonlinux -d microsoft/mssql-server-linux:2017-latest
```

在本示例中，端口 1421 已经在主机计算机上空闲。我们不能使用主机端口 1433，因为我们已经在运行一个 SQL Server 实例（在上一个练习中安装的）。第二个端口 1433 将是容器上的端口。

通过执行以下命令验证 SQL Server 2017 容器正在运行：

```bash
sudo docker ps -a
```

输出将显示类似此的内容，你可以通过检查 STATUS 来验证 SQL Server 容器已有效运行：

```text
CONTAINER          IMAGE                                     COMMAND
CREATED             STATUS                               PORTS      NAMES
33770544f5e6d       microsoft/mssql-server-linux   "/bin/sh -c /opt/mssql"   sqllinux
44 seconds ago      Up 35 seconds                             0.0.0.0:1433->tcp
```

如果你在同一台服务器上有 SQL Server 客户端工具，你可以直接连接到新安装。或者你可以像之前为 Ubuntu Linux 发行版那样安装它们。注意，只需要客户端工具，因为你将连接到运行在 Docker 容器中的 SQL Server 镜像。

你应该能够像之前指示的那样进行连接。例如，你可以使用主机端口 1421 使用以下命令：

```bash
/opt/mssql-tools/bin/sqlcmd -U sa
```

## 运行 SQL

此时运行 `SELECT @@VERSION` 显示如下内容：

```text
Microsoft SQL Server 2017 (RTM-CU2) (KB405274) - 14.0.3008.27 (X64)
Nov 16 2017 10:00:49
Copyright (C) 2017 Microsoft Corporation
Developer Edition (64-bit) on Linux (SUSE Linux Enterprise Server 12 SP2)
```

按照之前指示的相同步骤从虚拟机外部连接。

你需要在网络安全组上配置入站规则，允许使用 TCP 端口 1433 的 SQL Server 客户端连接。
