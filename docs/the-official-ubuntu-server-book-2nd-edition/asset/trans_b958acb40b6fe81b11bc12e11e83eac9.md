

```default install
label install
    menu label ^Install
    menu default
    kernel ubuntu-installer/i386/linux
    append vga=normal initrd=ubuntu-installer/i386/initrd.gz
ks=http://10.1.1.5/ks.cfg -- quiet
```

所以我们需要做的就是克隆 `label install` 部分两次，并调整每个部分以指向我们的其他 Kickstart 文件：

```default install
label install
    menu label ^Install
    menu default
    kernel ubuntu-installer/i386/linux
    append vga=normal initrd=ubuntu-installer/i386/initrd.gz
ks=http://10.1.1.5/ks.cfg -- quiet
label web
    menu label ^Install
    menu default
    kernel ubuntu-installer/i386/linux
    append vga=normal initrd=ubuntu-installer/i386/initrd.gz
ks=http://10.1.1.5/ks-web.cfg -- quiet
label mysql
    menu label ^Install
    menu default
    kernel ubuntu-installer/i386/linux
    append vga=normal initrd=ubuntu-installer/i386/initrd.gz
ks=http://10.1.1.5/ks-mysql.cfg -- quiet
```

正如你所见，我在每个部分中做的唯一实质性更改就是指向我创建的不同 Kickstart 文件。现在一旦我启动，我可以输入 web 或 mysql 然后按 Enter 来选择这些特定选项。

## Boot Cheat Codes

区分不同安装类型的另一种有用方法是使用 cheat codes（我借用自 Knoppix 的名称）。cheat code 是你在命令行上输入的选项，会传递给系统。关于启动提示符的有趣之处在于，启动提示符上的所有内容在安装过程中都可以通过 /proc/cmdline 文件访问。如果你想创建自定义 cheat codes，你所需要做的就是提供一个 pre- 或 post-install 脚本，该脚本解析 /proc/cmdline 并将这些设置存储到环境变量中。然后你可以在脚本中引用这些环境变量，并根据它们对 pre- 或 post-install 过程进行自定义更改。

例如，假设我们在启动提示符下定义两个 cheat codes：mytype，用于标记服务器类型（Web、MySQL、DNS），以及 myraid，用于指示是否应使用 RAID。与其设置三个不同的 Kickstart 文件，我可以使用单个 Kickstart 文件，该文件在 pre-installation 脚本中包含逻辑来解析这些选项并据此更改设置。以下是会解析 /proc/cmdline 文件、设置环境变量，然后根据它们执行特殊操作的示例 pre-install 脚本：

```%pre
for i in `cat /proc/cmdline` ; do
echo $i | grep -iq MYTYPE=
if [ $? -eq 0 ] ; then
export MYTYPE=`echo $i | awk -F"=" '{ print $2; }'`
fi
echo $i | grep -iq MYRAID=
if [ $? -eq 0 ] ; then
export MYRAID=`echo $i | awk -F"=" '{ print $2; }'`
fi
done

if [ $MYTYPE == "web" ]; then
# Change preseed settings for web servers
elif [ $MYTYPE == "mysql" ]; then
# Change preseed settings for mysql servers
elif [ $MYTYPE == "dns" ]; then
# Change preseed settings for dns servers
fi

if [ $MYRAID ]; then
# Change preseed settings for RAID
fi
```

现在在启动提示符下，如果我想设置一个带 RAID 的 MySQL 服务器，我可以输入 install mytype=mysql myraid=1。再次强调，这种方法的优点是它允许你维护单个 Kickstart 文件，该文件包含逻辑以根据特定服务器类型更改设置。这种方法的缺点是，随着时间的推移，结果的 Kickstart 文件可能会变得相当庞大和复杂。

## DHCP Selection

如果你的组织为服务器使用静态 DHCP 分配，这种方法尤其有效。使用静态 DHCP 租约，DHCP 服务器会根据主机的 MAC 地址，每次为请求 IP 地址的主机分配相同的 IP 地址。通常在此设置中，你的服务器在从网络启动时会自动安装新镜像。你会发现这种方法在大型集群或服务器在可能获得操作系统之前就已物理安装的环境中很受欢迎。一旦你将 pxelinux 配置更改为自动安装默认镜像，你的 DHCP 配置文件就会控制每个服务器最终会变成什么。管理员要做的就是将服务器连接到网络并打开电源，即可安装 Ubuntu。

在此场景中，你在 /var/lib/tftpboot 下创建多个目录，每个目录都包含 netboot.tar.gz 的解压副本。例如，如果我想为 Web、MySQL 和 DNS 服务器设置三个单独的配置，我可以执行以下操作：

```$ sudo cd /var/lib/tftpboot
$ sudo wget http://archive.ubuntu.com/ubuntu/dists/hardy/main/installer-i386/current/images/netboot/netboot.tar.gz
$ sudo mkdir web mysql dns
$ cd web
$ sudo tar -xzvf netboot.tar.gz
$ cd ../mysql
$ sudo tar -xzvf netboot.tar.gz
$ cd ../dns
$ sudo tar -xzvf netboot.tar.gz
```

现在我会更改这些子目录中每个 pxelinux.cfg/default 文件以反映我想要更改的任何特殊设置。此外，如果我想让此安装完全不需要用户交互，我将编辑 pxelinux.cfg/default 配置文件并将 TIMEOUT 值设置为 1，以便在一秒后自动开始安装过程。

