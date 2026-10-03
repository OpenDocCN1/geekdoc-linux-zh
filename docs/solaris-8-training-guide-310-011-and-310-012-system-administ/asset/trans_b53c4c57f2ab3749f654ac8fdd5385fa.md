
## 逐步操作
### 21.5 创建 JumpStart 客户端

执行以下步骤设置 JumpStart 客户端：

1. 在安装服务器上，切换到包含已安装的 Solaris 8 操作环境映像的目录，如下所示：

```
cd /export/jumpstart/Solaris_8/Tools
```

2. 使用本地目录中找到的 add_install_client 脚本创建 JumpStart 客户端，如下所示：

```
./add_install_client -s ultra5:/export/jumpstart/install \
-c ultra5://jumpstart -p ultra5://jumpstart -e 8:0:20:21:49:25 \
-i 192.168.1.106 client1 sun4u
```

系统响应如下：

```
Adding Ethernet number for client1 to /etc/ethers
Adding "share -F nfs -o ro,anon=0 /export/jumpstart/install" to /etc/dfs/dfstab
making /tftpboot
enabling tftp in /etc/inetd.conf
updating /etc/bootparams
copying inetboot to /tftpboot
```

add_install_client 脚本自动在以下文件和目录中创建了条目：

/etc/ethers
8:0:20:21:49:25  client1
/etc/dfs/dfstab
share -F nfs -o ro,anon=0 /export/jumpstart
/etc/bootparams
client1 root=ultra5:/export/jumpstart/Solaris_8/Tools/Boot install=ultra5:/export/jumpstart boottype= \
:in sysid_config=ultra5://jumpstart install_config=ultra5://jumpstart rootopts::rsize=32768
/tftpboot directory
lrwxrwxrwx 1 root other 26 Jun 19 16:11 C0A8016A -> inetboot.SUN4U.Solaris_8-1
lrwxrwxrwx 1 root other 26 Jun 19 16:11 C0A8016A.SUN4U -> inetboot.SUN4U.Solaris_8-1
-rw-r--r-- 1 root other 158592 Jun 19 16:11 inetboot.SUN4U.Solaris_8-1
-rw-r--r-- 1 root other 317 Jun 19 16:11 rm.192.168.1.106
lrwxrwxrwx 1 root other 1 Jun 19 16:11 tftpboot -> .

注意
在以下步骤中，示例中做了以下关联：
Install Server name          -server
Distribution directory - /export/jumpstart/install
Configuration Server name    -server
Configuration directory - /export/jumpstart/config
Boot server name             -server
Install client               -client1
Client architecture          -sun4m

3. 使用 rm_install_client 命令按如下方式从引导服务器中删除 JumpStart 客户端的条目和配置信息：

```
./rm_install_client client1
```

系统响应如下：

```
removing client1 from bootparams
removing /etc/bootparams, since it is empty
removing /tftpboot/inetboot.SUN4U.Solaris_8-1
removing /tftpboot
disabling tftp in /etc/inetd.conf
```

## 一个 JumpStart 安装示例

以下示例展示了如何为一个虚构站点设置自定义 JumpStart 安装。网络由一台 Enterprise 3000 服务器和五台 Sparc10 工作站组成。

## 设置安装服务器

第一步是设置安装服务器。您将选择企业服务器。这里存放 Solaris CD 的内容。CD 的内容可以通过将 CD 放入 CD-ROM 驱动器或将 CD 复制到服务器的本地硬盘来提供。对于本示例，您将把文件复制到本地硬盘。使用 setup_install_server 命令将 Solaris CD 的内容复制到服务器的本地磁盘。文件复制到 /export/install 目录。

## 逐步操作
### 21.6 设置安装服务器

按以下步骤创建安装服务器：

1. 将 Solaris 安装 CD 插入服务器的 CD-ROM 驱动器。

2. 输入以下内容：
```
cd /cdrom/cdrom0/s0/Solaris_8/Tools
./setup_install_server /export/install
```
系统响应如下：
```
Verifying target directory...
Calculating space required for the installation boot image
Copying Solaris_8 Tools hierarchy...
Install Server setup complete
```
3. 弹出 Solaris 8 安装 CD，并放入 Solaris 8 软件 1 of 2 CD。让 vold 自动挂载 CD。
4. 按如下方式切换到 CD 上的 Tools 目录：
```
cd /cdrom/cdrom0/Solaris_8/Tools
```
5. 按如下方式执行 add_to_install_server 脚本，将 CD 上的映像复制到 /export/install 目录：
```
./add_to_install_server /export/install
```
6. 使用标有 Solaris 8 软件 2 of 2 的 CD 重复此过程。

## 创建 JumpStart 目录

安装安装服务器后，您需要在服务器上设置一个 JumpStart 配置目录。此目录保存用于 Solaris 软件自定义 JumpStart 安装所需的文件。您通过从已放入 /export/install 的 Solaris CD 映像之一复制示例目录来设置此目录。输入以下内容执行此操作：

```
mkdir /jumpstart
cp -r /export/install/Solaris_8/Misc/jumpstart_sample /jumpstart
```

可以使用任何目录名。本示例将使用 /jumpstart。

## 设置配置服务器

## 逐步操作
### 21.7 设置配置服务器

下一步是设置配置服务器。按以下步骤操作：

1. 以 root 身份登录到要存放 JumpStart 配置目录的服务器。
2. 编辑 /etc/dfs/dfstab 文件。添加以下条目：
   `share -F nfs -o ro,anon=0 /jumpstart`
3. 输入 shareall 并按 Enter。这使 /jumpstart 目录的内容可供网络上的系统访问。
4. 使用之前复制到 JumpStart 目录中的示例类文件和规则文件，创建代表您网络的配置文件。对于本示例，我创建一个名为 engrg_prof 的类文件。其内容如下：

```
#Specifies that the installation will be treated as an initial
#installation, as opposed to an upgrade.
install_type initial_install
#Specifies that the engineering systems are standalone systems.
system_type standalone
#Specifies that the JumpStart software uses default disk
#partitioning for installing Solaris software on the engineering
#systems.
partitioning default
#Specifies that the developer's software group will be
#installed.
Cluster SUNWCprog
#Specifies that each system in the engineering group will have 50
#Mbytes of swap space.
filesys any 50 swap
```

注意
如果 NFS 服务器守护进程未运行，可能需要运行 /etc/init.d/nfs.server 启动脚本。有关更多信息，请参阅第 17 章，“The NFS Environment”。

规则文件包含以下规则：

```
network 192.9.200.0 - engrg_prof -
```

该规则文件说明 192.9.200.0 网络上的系统使用 engrg_prof 类文件进行安装。

5. 按如下方式验证规则和类文件：

```
cd /jumpstart
./check /usr/sbin/install.d/pfinstall -c /export/install engrg_prof
```

如果 check 未发现任何错误，它会创建 rules.ok 文件。

查找以下消息，表示 pfinstall 测试成功：

```
Installation complete
Test run complete. Exit status 0.
```

配置服务器的创建已完成。

## 设置客户端

现在，在安装服务器上，按如下方式设置每个客户端：

```
cd /export/install/Solaris_8/Tools
./add_install_client -s sparcserver://export/install \
-c sparcserver://jumpstart -p sparcserver://jumpstart \
-e 8:0:20:21:49:25 -i 192.9.200.106 sun1 sun4u
```

```
./add_install_client -s sparcserver://export/install \
-c sparcserver://jumpstart -p sparcserver://jumpstart \
-e 8:0:20:21:49:24 -i 192.9.200.107 sun2 sun4u
```

本示例设置了两台工程工作站 sun1 和 sun2，以便它们可以从名为 sparcserver 的安装服务器通过网络进行安装。

## 启动客户端

设置完成后，您可以在每个系统的 OK（PROM）提示符下使用以下启动命令启动工程系统：

```
boot net - install
```

您将在屏幕上看到以下显示内容：

```
Rebooting with command: net - install
Boot device: /iommu/sbus/ledma@f,400010/le@f,c00000  File and args: - install
20800
SunOS Release 5.8 Version Generic_108528-05 '32-bit
Copyright 1983-2000 Sun Microsystems, Inc.  All rights reserved.
whoami: no domain name
Configuring /dev and /devices
Using RPC Bootparams for network configuration information.
Configured interface le0
Using sysid configuration file 192.9.200.101:/jumpstart/sysidcfg
The system is coming up.  Please wait.
Starting remote procedure call (RPC) services: sysidns done.
Starting Solaris installation program...
Searching for JumpStart directory...
Using rules.ok from 192.9.200.101:/jumpstart.
Checking rules.ok file...
Using profile: engrg_prof
Executing JumpStart preinstall phase...
Searching for SolStart directory...
Checking rules.ok file...
Using begin script: install_begin
Using finish script: patch_finish
Executing SolStart preinstall phase...
Executing begin script "install_begin"...
Begin script install_begin execution completed.
Processing default locales
    - Specifying default locale (en_US)
Processing profile
    - Selecting cluster (SUNWCprog)
WARNING: Unknown cluster ignored (SUNWCxgl)
    - Selecting package (SUNWaudmo)
    - Selecting locale (en_US)
Installing 32 Bit Solaris Packages
- Selecting all disks
- Configuring boot device
- Configuring swap (any)
- Configuring /opt (any)
- Automatically configuring disks for Solaris operating environment
Verifying disk configuration
Verifying space allocation
    - Total software size: 401.60 Mbytes
Preparing system for Solaris install
Configuring disk (c0t3d0)
    - Creating Solaris disk label (VTOC)
Creating and checking UFS file systems
- Creating / (c0t3d0s0)
- Creating /opt (c0t3d0s5)
Beginning Solaris software installation
```
