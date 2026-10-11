
[root@client-server ~] grep -i "vmx" /proc/cpuinfo

flags : fpu pae mce cx8 apic ...[truncated]... vmx

```
The presence of `vmx` in this sample output shows that necessary CPU extensions are in place on the Intel processor.

While inside an AMD-based host system running Linux:

```
[root@amd-server ~] grep -i "svm" /proc/cpuinfo

flags : fpu vme pse 3dnowext ...[truncated]... svm
```
The presence of `svm` in this sample output shows that necessary CPU extensions are in place on the AMD processor.

If you're unsure what your host architecture is capable of, use the following command to test for either of the flags:
```bash
[root@ ~] egrep -oh '(vmx|svm)\w*' /proc/cpuinfo
```

# Installing the Virtualization Applications and Utilities

We are assuming that your host system is running any of the recent Linux distributions. You should therefore already have support for KVM built into your kernel. All that's left is to ensure you have all the supporting userland tools, utilities, and libraries installed for interacting with the KVM subsystem.

有多种工具可用于创建或管理虚拟机（VM）。我们将保持简单，使用现成的 `virt-install` way，它基于 `libvirt` C 语言库，从现有镜像配置新虚拟机。

按照以下步骤安装所需的应用程序：

- 1. 在基于 Fedora/CentOS/RHEL 的发行版上，使用 `dnf` 安装 `virt-install`：
```bash
[root@fedora-host #] dnf -y install virt-install
```

- 2. 在像 Ubuntu 等基于 Debian 的发行版上，你可以通过先运行以下命令安装包并加载必要的模块：
```bash
master@ubuntu-host:-$ sudo apt-get -y install qemu-kvm
```
然后使用 `modprobe` 命令加载适用于你平台的模块（`kvm-intel` 或 `kvm-amd`）。

- 3. 在启用 systemd 的 Fedora 发行版或较版本的 Debian 或 Ubuntu 上，你可以使用 `systemctl` 启动 `libvirtd` 服务：
```bash
[root@host #] systemctl start libvirtd
```

- 4. 在使用 systemd 作为服务管理器的 Linux 上，使用 `systemctl` 工具确保 `libvirtd` 服务在下次启动时自动启动：
```bash
[root@host #] systemctl enable libvirtd.service
```

- 5. 使用 `virsh` 工具确保系统上的虚拟化已启用并运行正常：
```bash
[root@host #] virsh list
Id      Name      State
------
```
只要之前的输出没有返回任何错误，你就没问题了。

## 下载并准备演示虚拟机镜像文件

原始的、未压缩的虚拟机镜像文件相当大。它包含了整个操作系统和应用程序列表。根据你的互联网连接和其他因素，你可能无法一次性下载整个镜像文件。由于这个原因，我们为你创建了两个版本的文件。第一个版本是一个近近 4GB 的单个大文件。第二个版本与第一个版本相似，不同之处在于将其分成了两个独立的较小文件。如果你选择使用较小文件，你必须在下载后将它们合并，以形成一个完整的虚拟机镜像文件。

让我们从下载和解压单文件的文件的步骤开始：

- 在我们的示例宿主机系统中，我们将与每个虚拟机相关的所有备用文件存储在自定义目录路径 `/home/vms` 下。
让我们创建该目录：
```
[root@host ~] # mkdir -p /home/vms/
```

- 将你的工作目录更改到 `/home/vms` 位置：
```
[root@host ~] # cd /home/vms/
```

- 你需要获取演示虚拟机镜像的准确下载位置（URL）。为了冗余起见，我们在几个网站上发布了这些信息（以防它们无法访问）。你可以使用你喜欢的 Web 浏览器通过访问以下任何一个网站来获取最新的/准确的下载位置：

- http://linuxserverexperts.com/7e/
- http://goo.gl/XsXhpi
- http://www.mhprofessional.com/sites/soykalinux
- http://goo.gl/vgc3Tc

- 一旦你找到了确切的下载链接，将链接复制到剪贴板（尝试右键点击最终链接并选择“复制链接……”之类的选项……）

- 在以下命令中将 `<DOWNLOAD-LINK>` 替换为正确的 URL：
```
[root@host ~] # wget -c -O abg-7e-vm.qcow2.tar.xz <DOWNLOAD-LINK>
```

例如，如果你从第一个网站获得的链接是 `http://linuxserverexperts.com/7e/abg-7e-vm.qcow2.tar.xz`，你可以通过运行 `wget` 程序来下载单文件：
```bash
[root@host ~] # wget -c -O abg-7e-vm.qcow2.tar.xz \
http://linuxserverexperts.com/7e/abg-7e-vm.qcow2.tar.xz
```

- 解压（提取并解压缩）你下载的镜像文件。输入
```bash
[root@host ~] # tar xvf abg-7e-vm.qcow2.tar.xz
```

- 一会儿之后，你应该得到一个单一虚拟机磁盘镜像文件。通过运行以下命令验证这一点：
```bash
[root@host ~] # ls -lh abg-7e-vm.qcow2
```

或者，如果你选择分两个文件下载虚拟机镜像，请遵循以下步骤：

- 创建存储虚拟机镜像的目录：
```bash
[root@host ~] # mkdir -p /home/vms/
```

# 790 Linux 系统管理：初学者指南

## 2. 将你的工作目录更改到 `/home/vms` 位置：
```bash
[root@host ~#] cd /home/vms/
```

## 3. 使用你喜欢的 Web 浏览器通过访问以下任何一个网站来获取最新的/准确的下载位置：

- http://linuxserverexperts.com/7e/
- http://goo.gl/XsXpi
- http://www.mhprofessional.com/sites/soinkalinux7
- http://goo.gl/vcgt3C

一旦你找到了下载链接，将链接复制到剪贴板（尝试点击最终链接并选择“复制链接……”之类的选项……）。

在下一步的命令中，将 `<DOWNLOAD-LINK>` 替换为正确的 URL。
```bash
[root@host ~#] wget -c -O abg-7e-vm.qcow2.tar.xz <DOWNLOAD-LINK>
```

## 4. 假设你从第一个网站获得的链接是 `http://linuxserverexperts.com/7e/abg-7e-vm.qcow2.tar.xz`，你可以使用 `wget` 程序来下载第一个文件：
```bash
[root@host ~#] wget -c -O abg-7e-vm.qcow2.tar.xz \
http://linuxserverexperts.com/7e/abg-7e-vm.qcow2.tar.xz
```
