
第一步是设置安装服务器。您将选择企业服务器。这里存放 Solaris CD 的内容。CD 的内容可以通过将 CD 放入 CD-ROM 驱动器或将 CD 复制到服务器的本地硬盘来提供。对于本示例，您将把文件复制到本地硬盘。使用 `setup_install_server` 命令将 Solaris CD 的内容复制到服务器的本地磁盘。文件复制到 `/export/install` 目录。

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

3. 弹出 Solaris 8 安装 CD，并放入 Solaris 8 软件 1 of 2 CD。让 `vold` 自动挂载 CD。

4. 按如下方式切换到 CD 上的 Tools 目录：

```
cd /cdrom/cdrom0/Solaris_8/Tools
```

5. 按如下方式执行 `add_to_install_server` 脚本，将 CD 上的映像复制到 `/export/install` 目录：

```
./add_to_install_server /export/install
```

6. 使用标有 Solaris 8 软件 2 of 2 的 CD 重复此过程。

## 创建 JumpStart 目录

安装安装服务器后，您需要在服务器上设置一个 JumpStart 配置目录。此目录保存用于 Solaris 软件自定义 JumpStart 安装所需的文件。您通过从已放入 `/export/install` 的 Solaris CD 映像之一复制示例目录来设置此目录。输入以下内容执行此操作：

```
mkdir /jumpstart
cp -r /export/install/Solaris_8/Misc/jumpstart_sample /jumpstart
```

可以使用任何目录名。本示例将使用 `/jumpstart`。

## 设置配置服务器

## 逐步操作

### 21.7 设置配置服务器

下一步是设置配置服务器。按以下步骤操作：

1. 以 `root` 身份登录到要存放 JumpStart 配置目录的服务器。

2. 编辑 `/etc/dfs/dfstab` 文件。添加以下条目：

   `share -F nfs -o ro,anon=0 /jumpstart`

3. 输入 `shareall` 并按 Enter。这使 `/jumpstart` 目录的内容可供网络上的系统访问。

4. 使用之前复制到 JumpStart 目录中的示例类文件和规则文件，创建代表您网络的配置文件。对于本示例，我创建一个名为 `engrg_prof` 的类文件。其内容如下：

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

如果 NFS 服务器守护进程未运行，可能需要运行 `/etc/init.d/nfs.server` 启动脚本。有关更多信息，请参阅第 17 章，“The NFS Environment”。

规则文件包含以下规则：

```
network 192.9.200.0 - engrg_prof -
```

该规则文件说明 192.9.200.0 网络上的系统使用 `engrg_prof` 类文件进行安装。

5. 按如下方式验证规则和类文件：

```
cd /jumpstart
./check /usr/sbin/install.d/pfinstall -c /export/install engrg_prof
```

如果 `check` 未发现任何错误，它会创建 `rules.ok` 文件。

查找以下消息，表示 `pfinstall` 测试成功：

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

本示例设置了两台工程工作站 `sun1` 和 `sun2`，以便它们可以从名为 `sparcserver` 的安装服务器通过网络进行安装。

## 启动客户端

设置完成后，您可以在每个系统的 OK（PROM）提示符下使用以下启动命令启动工程系统：

```
boot net - install
```

您将在屏幕上看到以下显示内容：
