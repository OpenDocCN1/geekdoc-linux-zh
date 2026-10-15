
### 如何操作...

首先，让我们通过以下步骤为我们的 `kickstart` 创建模板：

1. 首先，启动 `Kickstart Configurator`。
2. 从 `Kickstart Configurator` 中选择系统的基础配置。以下截图显示了你可以设置的选项：

   ![](img/a6dbf7df749be83c0faae2334e970c0b_776_0.png)

3. 现在，从 `Kickstart Configurator` 中选择安装方法。以下截图显示了你可以设置的选项：

   ![](img/a6dbf7df749be83c0faae2334e970c0b_777_0.png)

4. 接下来，将 `HTTP` 服务器和 `HTTP` 目录替换为你自己的值。

5. 确保引导程序应用了正确的设置。以下截图显示了引导程序的选项：

   ![](img/a6dbf7df749be83c0faae2334e970c0b_778_0.png)

6. 配置你的磁盘和分区信息。只需创建一个 `/boot` 分区即可！我们将手动编辑文件以进行更好的自定义。截图显示了分区信息视图中可以设置的选项：

   ![](img/a6dbf7df749be83c0faae2334e970c0b_779_0.png)

7. 配置你的网络。如果你想正确配置网络，你需要知道设备名称。以下截图显示了可以在网络配置视图中编辑的网络设备信息：

   ![](img/a6dbf7df749be83c0faae2334e970c0b_780_0.png)

8. 现在，禁用安装图形环境。

   我们希望包越少。以下截图显示了你在显示配置视图中可以设置的选项：

   ![](img/a6dbf7df749be83c0faae2334e970c0b_781_0.png)

### 批量部署 RHEL

9. 接下来，执行你认为必要的任何安装前和/或安装后任务。我总是尝试通过 `SSH` 和密钥来访问 `root` 用户。

   接收方的截图显示了你可以在“安装后脚本（Post-Installation Script）”视图中设置的选项：

   ![](img/a6dbf7df749be83c0faae2334e970c0b_782_0.png)

10. 保存 `kickstart` 文件。

11. 使用你喜欢的编辑器打开文件，并在你的分区部分添加以下内容：
    - `part.01 --size=1 --ondisk=sda --grow`
    - `voulgroup vg1 pv.01`
    - `logvol --vgname=vg1 --size=2048 --name=root`
    - `logvol /usr --vgname=vg1 --size=2048 --name=usr`
    - `logvol /var --vgname=vg1 --size=2048 --name=var`
    - `logvol /var/log --vgname=vg1 --size=1024 --name=var`
    - `logvol /home --vgname=vg1 --size=512 --name=home`
    - `logvol swap --vgname=vg1 --recommended --name=swap --fstype=swap`

12. 现在，在你的网络行中添加以下脚本：

    ```
    --hostname=rhel7
    ```

13. 在 `%post` 之前添加以下脚本：

    ```
    %packages -nobase

    %core --nodefaults

    %end
    ```

14. 为下一步创建一个密码哈希值，如下所示：

    ```
    # openssl passwd -1 "MySuperSecretRootPassword"

    $1$mecIlKXN$6VRdaRkevjw9nngcMtR10.
    ```

15. 保存生成文件。你应该得到类似这样的内容：

    ```
    #platform=x86, AMD64, or Intel EM64T

    #version=DEVEL

    # Install OS instead of upgrade

    install

    # Keyboard layouts

    keyboard 'be-latini'

    # Halt after installation

    halt

    # Root password

    rootpw --encrypted $1$mecIlKXN$6VRdaRkevjw9nngcMtR10.

    # System timezone

    timezone Europe/Brussels

    # Use network installation

    url="http://repo.example.com/rhel/7/os/x86_64//"

    # System language

    lang en_US

    # Firewall configuration

    firewall --disabled

    # Network information

    network --bootproto=static --device=enol

    gateway=192.168.0.254 --ip=192.168.0.1 --nameserver=192.168.0.253

    --netmask=255.255.255.0 --hostname=rhel7

    # System authorization information

    auth --useshadow --passalgo=sha512

    # Use text mode installation

    text

    # SELinux configuration

    selinux --forcing

    # Do not configure the X Window System

    skipx
    ```

### 批量部署 RHEL

```
# 系统引导加载程序配置

bootloader --location=none

# 清除主引导记录

zerombr

# 分区信息清除

clearpart --all --initlabel

# 磁盘分区信息

part /boot --ftype=xfs --ondisk=sda --size=512

part pv.01 --size=1 --ondisk=sda --grow

volroup vg1 pv.01

log / --name=vg1 --size=2048 --name=root --ftype=xfs

log /usr --name=vg1 --size=2048 --name=usr --ftype=xfs

log /var --name=vg1 --size=2048 --name=var --ftype=xfs

log /var/log --name=vg1 --size=1024 --name=var --ftype=xfs

log /home --name=vg1 --size=512 --name=home --ftype=xfs

log swap --name=vg1 --recommended --name=swap --ftype=xfs

%packages --nobase

@core --nodefaults

%end

%post

mkdir -p ~/.ssh

chmod 700 ~/.ssh

# 从我的密钥服务器下载我的授权密钥文件

server..

curl -O ~/.ssh/authorized_keys

https://keys.example.com/authorized_keys

chmod 600 ~/.ssh/authorized_keys

%end
```
