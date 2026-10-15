
# 第 27 章：转向云与容器

## 1. 安装并启动 podman 或 docker

```bash
# dnf install podman -y
# dnf install docker -y
# systemctl start docker
# systemctl enable docker
```

## 2. 使用 docker 或 podman 将此镜像拉取到本地 public.ecr.aws/docker/library/fedora

```bash
# podman pull public.ecr.aws/docker/library/fedora
# docker pull public.ecr.aws/docker/library/fedora
```

## 3. 运行 fedora 镜像打开 bash shell

```bash
# podman run -it fedora bash
# docker run -it fedora bash
```

## 4. 运行命令查看容器的基础操作系统，安装 proc-ps 包并运行命令查看容器内部运行的进程

```bash
bash-4.4# cat /etc/os-release | grep NAME="Fedora Linux"
bash-4.4# dnf install proc-ps -y
bash-4.4# ps -ef
```

| UID | PID | PPID | C | TTY | TIME | CMD |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| root | 1 | | 03:37 | pts/0 | 00:00:00 | bash |
| root | 20 | 1 | 03:43 | pts/0 | 00:00:00 | ps -ef |

## 5. 使用交互式 shell 重启并连接你刚刚关闭的容器

```bash
# podman ps -a
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
2a37d41fb734 ..latest bash 7 minutes ago Exited (0) 4 seconds
# podman start 2a37d41fb734
bash-4.4# exit
```

## 6. 从 fedora 基础镜像创建一个简单的 Dockerfile，包含一个名为 cworks.sh 的脚本，输出 "The Container Works!"，并将该脚本添加到镜像中运行

### a. 创建并进入目录

```bash
# mkdir project
# cd project
```

### b. 创建如下内容的 Dockerfile 文件

```dockerfile
FROM public.ecr.aws/docker/library/fedora
COPY cworks.sh /usr/local/bin/
CMD ["/usr/local/bin/cworks.sh"]
```

### c. 创建内容如下的 cworks.sh 文件

```bash
#!/bin/bash
set -o errexit
echo "The Container Works!"
```

# 附录 B：练习答案

```bash
set -o nounset
set -o pipefail
echo "The Container Works!*"
```

## 7. 使用 docker 或 podman 根据你创建的 Dockerfile 构建一个名为 `containerworks` 的镜像

```bash
# podman build -t myproject
# docker build -t myproject
```

## 8. 要访问容器注册表，可以通过从 Fedora 安装 `docker-distribution` 软件包，或者在 Quay.io 或 Docker Hub 上获取账户

```bash
# dnf install docker-distribution -y
# systemctl start docker-distribution
# systemctl enable docker-distribution
```

或者从 Quay.io (https://quay.io/plans/) 或 Docker Hub 获取账户，然后执行：

```bash
# podman login quay.io
Username: <username>
Password: *************
```

## 9. 将新镜像标记并推送到指定的容器注册表

```bash
# docker images | grep myproject
myproject latest a2c3a4c0a4a 15 minutes ago 169 MB
# podman tag a2c3a4c0a4a localhost:5000/myproject:v1.0
# podman push localhost:5000/myproject:v1.0
```

# 第 28 章：使用 Linux 进行云计算

## 1. 检查你的电脑是否支持 KVM 虚拟化

输入 `vmx svm`：

```bash
# /proc/cpuinfo | grep --color -E "vmx|svm"
flags fpu vme de start mtr tsr cx apic sep sse ss ht tm 
pge cmov cmov pat pse32 clflush dts acpi fxr sse s22 ht
syscall nx86 pdgelb dr_is constant_tsc aperfperf t pcimiulqd gdq dtes64
bt rep_group topology nonstop_tsc monitor ds_cpl vmx smx...
```

CPU 必须支持 `vmx` 或 `svm` 之一。`lm` 表示这是一台 64 位的计算机。

## 2. 安装 Linux 系统以及将其用作 KVM 主机和运行虚拟机管理器（Virtual Machine Manager）应用程序所需的软件包

### a. 从 Linux 网站（例如 fedoraproject.org）获取实时镜像或安装镜像，并将其刻录 USB 驱动器或 DVD（或通过其他方式使其可用）。

### b. 启动安装镜像，并将其安装到硬盘。

### c. 对于 Fedora Workstation，在安装完成并重启后，安装以下软件包（适用于不同的 Linux 发行版），你可能还需要安装一个提供 `libvirt` 的软件包：

```bash
# dnf install libvirt libvirt-daemon-config-network
```

## 3. 要确保 `sshd` 和 `libvirtid` 服务在系统上运行

```bash
# systemctl start sshd.service
# systemctl enable sshd.service
# systemctl start libvirtid.service
# systemctl enable libvirtid.service
```

## 4. 获取与你的虚拟机程序兼容的 Linux 安装 ISO 镜像，并拷贝到虚拟机管理器用于存储镜像的默认目录

例如，如果 Fedora Workstation DVD 位于当前目录：

```bash
# cp Fedora-Workstation-Live-42-1.1.x86_64.iso \
# /var/lib/libvirt/images/
```

## 5. 要检查网络桥接（virbr0）上的设置

```bash
# ip addr show virbr0
virbr0:<NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state UP group default
link/ether 02:21:23:0e:2b:c1 brd ff:ff:ff:ff:ff:ff
inet 192.168.122.1/24 brd 192.168.122.255 scope global virbr0 valid_lft forever preferred left forever
```

## 6. 使用你上方拷贝的 ISO 安装虚拟机

### a. 输入此命令：

```bash
# virt-manager &
```

### b. 选择“文件”（File），然后选择“新建虚拟机”（New Virtual Machine）。

### c. 选择“本地安装媒体”（Local Install Media）并点击“下一步”。

### d. 选择“浏览”（Browse），选择实时或安装 ISO，点击“选择卷”（Choose Volume），并点击“下一步”。

### e. 选择内存和 CPU 并点击“下一步”。

### f. 选择你想要使用的磁盘大小并点击“下一步”。

### g. 选择“客户虚拟机网络默认：NAT”（Guest Virtual Network Default: NAT）（它可能已经被选中）。

### h. 如果看起来没，点击“完成”（Finish）。

### i. 按照安装 ISO 指出的安装过程进行。

## 7. 确保你执行了以下操作

### a. 双击新虚拟机的条目。

### b. 当查看窗口出现时，像平时一样登录。

## 8. 检查你的虚拟机是否可以连接到互联网或虚拟机程序的网络端

执行以下操作之一：

### a. 打开网络浏览器，尝试连接到互联网上的网站。

### b. 打开终端窗口，输入 `ping redhat.com`，然后按 Ctrl+C。

## 9. 停止虚拟机

### a. 在虚拟机管理器中右键点击虚拟机，选择“关闭”或“强制关闭”。

### b. 或在虚拟机内部执行 `shutdown` 命令。

## 10. 重启虚拟机

### a. 在虚拟机管理器中右键点击虚拟机，选择“运行”或“启动”。

# 第 29 章：部署 Linux

## 1. 获取与你的虚拟机程序兼容的 Linux 安装 ISO 镜像，并拷贝到虚拟机管理器用于存储镜像的默认目录

例如，如果 Fedora Workstation DVD 位于当前目录：

```bash
# cp Fedora-Workstation-Live-42-1.1.x86_64.iso \
# /var/lib/libvirt/images/
```

## 2. 要检查网络桥接（virbr0）上的设置

```bash
# ip addr show virbr0
virbr0:<NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state UP group default
link/ether 02:21:23:0e:2b:c1 brd ff:ff:ff:ff:ff:ff
inet 192.168.122.1/24 brd 192.168.122.255 scope global virbr0 valid_lft forever preferred left forever
```

## 3. 使用你上方拷贝的 ISO 安装虚拟机

### a. 输入此命令：

```bash
# virt-manager &
```

### b. 选择“文件”（File），然后选择“新建虚拟机”（New Virtual Machine）。

### c. 选择“本地安装媒体”（Local Install Media）并点击“下一步”。

### d. 选择“浏览”（Browse），选择实时或安装 ISO，点击“选择卷”（Choose Volume），并点击“下一步”。

### e. 选择内存和 CPU 并点击“下一步”。

### f. 选择你想要使用的磁盘大小并点击“下一步”。

### g. 选择“客户虚拟机网络默认：NAT”（Guest Virtual Network Default: NAT）（它可能已经被选中）。

### h. 如果看起来没，点击“完成”（Finish）。

### i. 按照安装 ISO 指出的安装过程进行。

## 7. 确保你执行了以下操作

### a. 双击新虚拟机的条目。

### b. 当查看窗口出现时，像平时一样登录。

## 8. 检查你的虚拟机是否可以连接到互联网或虚拟机程序的网络端

执行以下操作之一：

### a. 打开网络浏览器，尝试连接到互联网上的网站。

### b. 打开终端窗口，输入 `ping redhat.com`，然后按 Ctrl+C。

## 9. 停止虚拟机

### a. 在虚拟机管理器中右键点击虚拟机，选择“关闭”或“强制关闭”。

### b. 或在虚拟机内部执行 `shutdown` 命令。

## 10. 重启虚拟机

### a. 在虚拟机管理器中右键点击虚拟机，选择“运行”或“启动”。

# 第 30 章：使用 Ansible 自动化应用和基础设施

## 1. 获取与你的虚拟机程序兼容的 Linux 安装 ISO 镜像，并拷贝到虚拟机管理器用于存储镜像的默认目录

例如，如果 Fedora Workstation DVD 位于当前目录：

```bash
# cp Fedora-Workstation-Live-42-1.1.x86_64.iso \
# /var/lib/libvirt/images/
```

## 2. 要检查网络桥接（virbr0）上的设置

```bash
# ip addr show virbr0
virbr0:<NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state UP group default
link/ether 02:21:23:0e:2b:c1 brd ff:ff:ff:ff:ff:ff
inet 192.168.122.1/24 brd 192.168.122.255 scope global virbr0 valid_lft forever preferred left forever
```

## 3. 要安装 ansible 软件包

### Fedora

```bash
# dnf install ansible -y
```

### Ubuntu

```bash
sudo apt update
sudo apt install software-properties-common
sudo apt add-repository --yes ppa:ansible
sudo apt install ansible
```

## 2. 为运行 Ansible 的用户添加 sudo 权限，创建一个如下的项目（将 joe 更改为你的用户名）

```
joe ALL=(ALL) NOPASSWD: ALL
```

## 3. 打开名为 `my_playbook.yaml` 的文件并添加内容

```yaml
---
name: Create web server
hosts: localhost
tasks:
  name: Install httpd
    yum:
      name: httpd
      state: present
```

## 4. 以检查模式运行 my_playbook.yaml 剧本，用户没有权限（它应该失败，因为用户没有安装软件包）

```bash
$ ansible-playbook -C my_playbook.yaml
```
