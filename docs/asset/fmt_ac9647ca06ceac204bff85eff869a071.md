
```bash
lb@rhel9_byp ~$ dotnet run --project my-app
```

输出应为 `Hello World!`

### 使用 .NET 6.0 发布应用程序

发布方法如下：

- 单文件应用程序：部署为单个可执行文件。此方法将你的应用程序及其所有依赖项打包成单个可执行文件。它通过减少需要分发和管理的文件数量来简化部署。然而，由于必要的依赖项被打包在一起，可能会导致文件大小较大。
- 框架依赖部署 (`FDD`)：使用共享的系统级 `.NET` 版本。在这种方法中，你的应用程序依赖于共享的系统级 `.NET` 运行时。这意味着你的应用程序包不包含 `.NET` 运行时，使得应用程序体积更小。缺点是目标系统必须安装适当版本的 `.NET` 运行时。
- 自包含部署 (`SCD`)：在部署中包含 `.NET`。此方法将与你的应用程序一起安装的 `.NET` 运行时打包，使其能够独立于目标系统上安装的 `.NET` 版本进行运行。这确保了兼容性并简化了部署，但代价是由于包含了 `.NET` 运行时，包的体积会更大。
- 1. 发布应用程序：

```bash
lb@rhel9_byp ~$ dotnet publish my-app -f net6.0 -c Release
```

- 2. 可选：为 RHEL 裁剪依赖项：

```bash
lb@rhel9_byp ~$ dotnet publish my-app -f net6.0 -c Release -r rhel.9-x64 --self-contained false
```

### 在容器中运行 .NET 应用程序

要在 RHEL 容器中部署 `.NET` 应用程序，请遵循以下步骤。此方法使用 `.NET` 运行时和 `Podman` 等容器工具来实现高效的部署流水线。

- 1. 创建并发布一个新的 MVC 项目：

[lb@rhel19_bvp ~]$ `dotnet new mvc --output mvc_runtime_example`

[lb@rhel19_bvp ~]$ `dotnet publish mvc_runtime_example -f net6.0 -c Release`

- 2. 创建 `Dockerfile`：

[lb@rhel19_bvp ~]$ `cat > Dockerfile <<EOF`

FROM registry.access.redhat.com/ubi8/dotnet-60-runtime

ADD bin/registry/net6.0/publish/.

CMD "dotnet", "mvc_runtime_example.dll"

EOF

- 3. 构建并运行容器：

[lb@rhel19_bvp ~]$ `podman build -t dotnet-60-runtime-example`

[lb@rhel19_bvp ~]$ `podman run -d -p 8080:8080 dotnet-60-runtime-example`

- 4. 验证应用程序：

[lb@rhel19_bvp ~]$ `xdg open http://127.0.0.1:8080`

## 方案 #69：安装并配置 GIT 仓库

要在 RHEL 系统上安装和配置 Git 仓库，请遵循以下详细步骤。本指南假设你在 RHEL 系统上拥有管理员权限。

### 安装 Git

- 1. 安装 Git：

使用 `yum` 包管理器安装 `Git`：

[lb@rhel19_bvp ~]$ `sudo yum install -y git`

- 2. 验证安装：

检查已安装的 `Git` 版本以确保其正确安装：

```bash
[lb@rhel9_bpp ~]$ git -version
git version 2.39.3
```

## 配置 Git

- 1. 设置你的 Git 用户信息：

配置你的姓名和邮箱地址。这些信息将用于你的提交（`commits`）中。

```bash
[lb@rhel9_bpp ~]$ git config --global user.name "Your Name"
[lb@rhel9_bpp ~]$ git config --global user.email your.email@example.com
```

- 2. 验证配置：

检查你的 `Git` 配置以确保用户信息已正确设置：

```bash
[lb@rhel9_bpp ~]$ git config --list
```

## 初始化 Git 仓库

- 1. 为你的 Git 仓库创建一个新目录：

为你的项目创建一个目录，或导航到现有项目：

```bash
[lb@rhel9_bpp ~]$ mkdir ~/my-git-repo
[lb@rhel9_bpp ~]$ cd ~/my-git-repo
```

- 2. 初始化 Git 仓库：

在目录中初始化一个新的 Git 仓库：

```bash
[lb@rhel9_bpp ~]$ git init
```

- 3. 验证仓库初始化：

检查目录内容以确保已创建了 `.git` 目录：

```bash
[lb@rhel9_bpp ~]$ ls -a
```

## 创建并提交到仓库

- 1. 在你的仓库中创建一个新文件：

创建一个创建一个示例文件并添加到仓库：

```bash
[lb@rhel9_bpp ~]$ echo "# My Repository" > README.md
```

- 2. 将文件添加到暂存区：

使用 `git add` 命令将文件添加到暂存区：

```bash
[lb@rhel9_bpp ~]$ git add README.md
```

- 3. 将文件提交到仓库：

带有描述信息将文件提交到仓库：

```bash
[lb@rhel9_bpp ~]$ git commit -m "Initial commit"
```

- 4. 验证提交：

检查提交历史以确保你的文件已提交：

```bash
[lb@rhel9_bpp ~]$ git log
```

## 设置远程仓库

如果你想设置远程仓库，可以使用 `GitHub`、`GitLab` 和 `Bitbucket` 等平台。以下是使用 `GitHub` 的示例。

- 1. 在 GitHub 上创建一个新仓库：

访问 `GitHub` 并创建一个新仓库。不要初始化 `.gitignore` 文件。
- 2. 添加远程仓库：

将你的 `GitHub` 仓库 `URL` 作为远程仓库：

```bash
[lb@rhel9_bpp ~]$ git remote add origin https://github.com/yourusername/your-repo.git
```

- 3. 将本地仓库推送到远程仓库：

将本地仓库的提交推送到 `GitHub`：

```bash
[lb@rhel9_bpp ~]$ git push -u origin master
```

## Recipe：安装并配置 DevOps 工具

要在 RHEL 9 系统上安装并配置必要的 DevOps 工具，请遵循以下步骤。本指南涵盖了 `Git`、`Jenkins` 和 `Kubernetes`（通过 `minikube`）以及必要的配置。假设你拥有 RHEL 系统的管理权限。

## Jenkins

- 1. 添加 Jenkins 仓库：

```bash
[lb@rhel9_bpp ~]$ sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.key
```

- 2. 安装 Jenkins：
- 3. 启动并启用 Jenkins 服务：

```bash
[lb@rhel9_bpp ~]$ sudo systemctl start jenkins
[lb@rhel9_bpp ~]$ sudo systemctl enable jenkins
```

- 4. 调整防火墙：

```bash
[lb@rhel9_bpp ~]$ sudo firewall-cmd --permanent --zone=public --add-port=8080/tcp
[lb@rhel9_bpp ~]$ sudo firewall-cmd --reload
```

- 5. 访问 Jenkins：

打开浏览器并访问 `http://your_server_ip:8080` 完成 `Jenkins` 设置。

## Docker

- 1. 添加 Docker 仓库：

```bash
[lb@rhel9_bpp ~]$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

- 2. 安装 Docker：

```bash
[lb@rhel9_bpp ~]$ sudo yum install -y docker-ce docker-ce-cli containerd.io
```
