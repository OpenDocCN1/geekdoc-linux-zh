
### 3. 启动并启用 Docker 服务

```bash
[lb@rhel9_bpp ~]$ sudo systemctl start docker
[lb@rhel9_bpp ~]$ sudo systemctl enable docker
```

### 4. 将用户加入 docker 组

```bash
[lb@rhel9_bpp ~]$ sudo usermod -aG docker $USER
newgrp docker
```

### 5. 验证 Docker 安装

```bash
[lb@rhel9_bpp ~]$ docker -version
Docker version 25.0.2, build 29cf629
```

## Ansible

### 1. 安装 Ansible

```bash
[lb@rhel9_bpp ~]$ sudo yum install -y ansible-core
```

### 2. 验证 Ansible 安装

```bash
[lb@rhel9_bpp ~]$ ansible --version
ansible [core 2.17.1]
```

## Kubernetes (minikube)

### 1. 安装 Minikube 依赖

源代码、DevOps 流水线和应用开发

### 2. 下载并安装 minikube

```bash
[lb@rhel19_bpp ~]$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

### 3. 启动 minikube

```bash
[lb@rhel19_bpp ~]$ minikube start --driver=none
```

### 4. 验证 minikube 安装

```bash
[lb@rhel19_bpp ~]$ minikube status
```

## Kubernetes (kubectl)

### 1. 下载并安装 kubectl

```bash
[lb@rhel19_bpp ~]$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/kubectl
```

### 2. 验证 kubectl 安装

```bash
[lb@rhel19_bpp ~]$ kubectl version
```

## Recipe #71：安装并配置 DevOps 核心工具

源代码、DevOps 流水线和应用开发

## Ansible

### 1. 安装 Ansible

从默认仓库安装 Ansible：

```bash
[lb@rhel9_bpp ~]$ sudo dnf install ansible-core
```

### 2. 验证 Ansible 安装

检查 Ansible 版本以确保已正确安装：

```bash
[lb@rhel9_bpp ~]$ ansible --version
```

## 配置 Ansible

### 1. 为你的 Ansible 创建目录

为你的项目创建一个目录：

```bash
[lb@rhel9_bpp ~]$ mkdir ~/ansible
[lb@rhel9_bpp ~]$ cd ~/ansible
```

### 2. 创建清单文件

清单文件列出了 Ansible 要管理的主机：

```bash
[lb@rhel9_bpp ~]$ vi hosts
```

添加以下内容：

```
[webservers]
webserver1=192.168.1.10
webserver2=192.168.1.11

[dbservers]
dbserver1=192.168.1.20
```

### 3. 创建基础 Ansible 配置

在同一目录下创建一个名为 `ansible.cfg` 文件：

```bash
[lb@rhel9_bpp ~]$ vi ansible.cfg
```

添加以下内容：

```ini
[defaults]
inventory = ./hosts
remote_user = root
host_key_checking = False
```

## 创建 Ansible playbook

### 1. 创建 playbook 文件

`playbook` 定义了在主机上执行的任务。创建一个名为 `site.yml` 的文件：

```bash
[lb@rhel9_bpp ~]$ vi site.yml
```

### 2. 为 playbook 添加任务

添加以下内容作为在 `webservers` 上安装 Apache 的 `site.yml`：

```yaml
---
- name: Install and configure Apache
  hosts: webservers
  tasks:
    - name: Install Apache
      ansible.builtin.yum:
        name: httpd
        state: present
    - name: Start and enable Apache
      ansible.builtin.systemd:
        name: httpd
        state: started
        enabled: yes
    - name: Copy index.html to webservers
      ansible.builtin.copy:
        src: ./files/index.html
        dest: /var/www/html/index.html
```

### 3. 创建 index.html 文件

创建一个由 Ansible 部署的简单 HTML 文件：

```bash
[lb@rhel9_bpp ~]$ mkdir files
[lb@rhel9_bpp ~]$ vi files/index.html
```

添加以下内容：

```html
<html>
<head>
  <title>Welcome to Ansible Managed Server</title>
</head>
<body>
  <h1>It works!</h1>
</body>
</html>
```

## 运行 Ansible playbook

### 1. 运行 playbook

使用以下命令执行 playbook：

```bash
[lb@rhel9_bpp ~]$ ansible-playbook site.yml
```

### 2. 验证部署

`playbook` 成功运行后，验证 Apache 是否在 Web 服务器上安装并运行，以及自定义的 `index.html` 是否已部署。打开浏览器并访问 web 服务器的 IP 地址以查看更改。

## 总结

本章介绍了了在 RHEL 环境中开发、部署和管理应用的多种核心工具和技术。我们从安装 OpenJDK JRE 版本 8、11、17 和 21 的详细步骤开始，包括

.NET 6.0 SDK、创建和运行 .NET 以及探索各种发布方法。接下来，我们涵盖了 Git 的安装与配置、设置并初始化仓库、提交文件以及配置 GitHub 上的远程仓库。我们还讨论了关键 DevOps 工具的安装与配置，例如用于 CI/CD 的 Jenkins、用于容器化的 Docker、用于自动化的 Ansible、用于集群调度的 Kubernetes (`minikube`) 以及 Kubernetes 命令行 (`kubectl`)。最后，我们提供了关于设置 Ansible 实现 DevOps 流水线自动化的详细指南，包括创建清单文件、配置文件以及编写剧本来自动化在 Web 服务器上安装和配置 Apache 等任务。

在下一章中，我们将讨论集群和服务器的管理，重点是高可用（HA）环境的搭建与管理。主题包括为 Apache 和 NFS 服务器配置主/备集群、管理集群资源和节点，以及在 RHEL 上使用 Pacemaker 确保具有韧性的服务连续性。

## 记忆点

- `JRE` 和 `JDK`: `JRE` 提供了运行 Java 应用程序所需的库，而 `JDK` 包含了用于开发 Java 应用程序的工具。

- `.NET Framework`: `.NET` 是一个多功能开发平台，支持多种部署方法，包括单文件部署、框架依赖部署和自部署。

- `Git`: `Git` 是一个分布式版本控制系统，对于跟踪代码更改和与其他人员协作至关重要。它涉及初始设置、仓库创建以及为协作开发配置远程仓库。

- `Jenkins`: `Jenkins` 是一个用于促进 CI/CD 的开源自动化服务器。它需要设置仓库、配置防火墙规则并访问 Web 界面进行配置。
