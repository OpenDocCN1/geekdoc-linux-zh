
它将安装的操作系统（套件）。下面是我们将基于其构建的命令的第一段（但现在先别按回车）：

```
$ sudo vmbuilder kvm ubuntu
```

你可以根据所选的管理程序和套件选择不同的选项，并且可以在每个选项后传递--help参数以获取特定选项列表：

```
$ sudo vmbuilder kvm ubuntu --help
```

vmbuilder脚本会在当前目录下创建一个目录，并将VM的磁盘文件放在那里。因此，如果你在磁盘上划出了专门存放VM文件的地方，请务必先切换到该目录。下面是一个相对基本的vmbuilder命令示例，它将创建一个名为test1的Ubuntu Lucid VM：

```
$ sudo vmbuilder kvm ubuntu --suite lucid --flavour virtual --arch i386 --hostname test1 --libvirt qemu:///system --rootsize=2048 --swap size=256 --user ubuntu --pass insecure -d test1-kvm
2010-04-17 12:17:04,193 INFO : Calling hook: preflight_check
2010-04-17 12:17:04,196 INFO : Calling hook: set_defaults
2010-04-17 12:17:04,197 INFO : Calling hook: bootstrap
...
2009-02-27 16:52:31,480 INFO    Cleaning up
```

运行该命令后，脚本会自行获取所需的全部包和文件，并自动为我构建VM。下面我来逐一描述我所选择的每个选项：

- **--suite lucid**
  --suite选项用于选择要安装的Ubuntu版本。我这里选择了lucid，但你也可以选择dapper、feisty、gutsy、hardy、intrepid、jaunty或karmic。

- **--flavour virtual**
  Ubuntu提供了多种不同的内核风格。virtual风格会选择针对VM优化的JeOS内核，但你可选择的内核种类还有很多，具体取决于你选择的Ubuntu套件和架构。

- **--arch i386**
  这是用于我的VM的处理器架构。如果我不指定它，默认将使用宿主机架构。有效选项为`i386`、`amd64`和`lpia`。

- **--hostname test1**
  如果不指定主机名，VM将默认为主机名ubuntu。当你决定创建多个VM时，这就会出问题，此时你会得到错误提示：域ubuntu已存在。使用`--hostname`选项，这样你不仅可以指定操作系统内部的主机名，还可以指定将注册到KVM中的唯一名称。

- **--libvirt qemu:///system**
  `--libvirt`选项会自动将此VM添加到我的本地KVM实例中。

- **--rootsize 2048 和 --swapsize 256**
  对于基本VM，你可能只希望有一个包含根分区和交换分区的单一磁盘。在这种情况下，你可以使用`--rootsize`和`--swapsize`以兆字节为单位指定根分区和交换分区的大小。还有一个`--optsize`选项可以设置单独的/opt分区。

- **--user ubuntu 和 --pass insecure**
  你会希望系统上有某种默认用户，这样构建完成后你就可以登录，除非你的网络使用LDAP或其他网络认证。`--user`和`--pass`参数让我可以指定要使用的默认用户和密码；否则两者都会默认为ubuntu。你还可以使用`--name`选项来设置用户的全名。

- **-d test1-kvm**
  默认情况下，`vm-builder`会将VM的根磁盘安装在用户主目录下的ubuntu-kvm目录中。当然，一旦你设置了一个VM，你将无法重用同一个目录，因此`-d`选项允许你指定目标目录的位置。

安装完成后，我会看到当前目录下创建了一个新的test1-kvm目录，里面是该VM的磁盘文件：

```bash
$ ls test1-kvm/
run.sh tmpHHSJGZ.qcow2
```

此外，我的新VM将被注册到KVM，其定义设置的XML文件将安装在/etc/libvirt/qemu/test1.xml下，内容类似于：

```xml
<domain type='kvm'>
  <name>test1</name>
  <uuid>907a0091-e31f-ef2b-6181-dc2d1225ed65</uuid>
  <memory>131072</memory>
  <currentMemory>131072</currentMemory>
  <vcpu>1</vcpu>
  <os>
    <type arch='i686' machine='pc-0.12'>hvm</type>
    <boot dev='hd'/>
  </os>
  <features>
    <acpi/>
  </features>
  <clock offset='utc'/>
  <on_poweroff>destroy</on_poweroff>
  <on_reboot>restart</on_reboot>
  <on_crash>destroy</on_crash>
  <devices>
    <emulator>/usr/bin/kvm</emulator>
    <disk type='file' device='disk'>
      <source file='/home/ubuntu/vms/test1-kvm/tmpHHSJGZ.qcow2'/>
      <target dev='hda' bus='ide'/>
    </disk>
    <interface type='network'>
      <mac address='52:54:00:c6:18:b7'/>
      <source network='default'/>
      <model type='virtio'/>
    </interface>
    <input type='mouse' bus='ps2'/>
    <graphics type='vnc' port='-1' autoport='yes' listen='127.0.0.1'/>
    <video>
      <model type='cirrus' vram='9216' heads='1'/>
    </video>
  </devices>
</domain>
```
