
分区文件的语法对于此脚本的正常运行至关重要。此文件用于构建 sfdisk 命令的输入文件。每行包含设备名称、起始点、分区大小（以兆字节为单位）、分区类型、指示分区是否应标记为活动的一个标志，最后是最终的挂载点以及指示应挂载顺序的序列号。以下是示例分区文件。请注意，在此文件中，您指定了 /dev/sda4 分区，但未为其提供任何值。这是满足 sfdisk 命令的要求。

```
1,1024,L,*,/,1
2,128,S,,,
3,,E,,,
4,,,
5,1024,L,/,usr,2
6,,L,,/var,3
```

上面的示例文件在 /dev/sda1 上创建了一个 1024 兆字节的分区，分区类型为 L（代表 Linux 原生），并将其标记为活动。然后在 /dev/sda2 上创建一个类型为 S 的交换分区，大小为 128 兆字节。下一个分区类型为 E，即扩展分区，由于未指定大小，因此占用磁盘剩余空间。现在您指定 /dev/sda4，其大小、起始位置或类型均无值。此分区实际上不存在，但必须指定以满足 sfdisk。下一个真实分区是 /dev/sda5，它是一个类型为 L 的逻辑驱动器，大小为 1024 兆字节。最后一个分区是 /dev/sda6，它也是类型 L，并占用扩展分区的剩余空间。使用此示例分区文件和第 3.2 节中的脚本会生成以下输出：

```
[root@quicksilver chapter3]# ./dprepare -t nomad -b hda -p partfile

Disk /dev/hda: 128 heads, 63 sectors, 785 cylinders

Old situation:
Units = megabytes of 1048576 bytes, blocks of 1024 bytes, counting from 0
```

| 设备 | 启动 | 开始 | 结束 | MB | #块 | Id | 系统 |
|---|---|---|---|---|---|---|---|
| /dev/sda1 |  | 0* | 1536- | 1536- | 1572448* | b | Win95 FAT32 |
| /dev/sda2 | * | 1535+ | 3027- | 1493- | 1528128 | 83 | Linux |
| /dev/sda3 |  | 3027+ | 3090- | 63 | 64512 | 82 | Linux swap |
| /dev/sda4 |  | 0 | - | 0 | 0 | 0 | Empty |

新情况：
单位 = 1048576 字节的兆字节，1024 字节的块，从 0 开始计数

| 设备 | 启动 | 开始 | 结束 | MB | #块 | Id | 系统 |
|---|---|---|---|---|---|---|---|
| /dev/sda1 | * | 0+ | 1027- | 1028- | 1052351* | 83 | Linux |
| /dev/sda2 |  | 1027+ | 1157- | 130- | 133056 | 82 | Linux swap |
| /dev/sda3 |  | 1157+ | 3090- | 1934- | 1978212 | 5 | Extended |
| /dev/sda4 |  | 0 | - | 0 | 0 | 0 | Empty |
| /dev/sda5 |  | 1157+ | 2185- | 1028- | 1052351+ | 83 | Linux |
| /dev/sda6 |  | 2185+ | 3699- | 906- | 927359+ | 83 | Linux |

执行 mke2fs /dev/sda1
执行 mkswap /dev/sda2
执行 mke2fs /dev/sda5
执行 mke2fs /dev/sda6

## 安装操作系统映像

现在您有一些可用的文件系统，您可以挂载它们并使用之前创建的安装映像，通过网络将操作系统传输到新系统。映像是一个 afio 归档文件，安装过程只是将归档文件解包到标准输出，然后通过管道传递给 rsh 命令，该命令将数据写入远程系统上准备好的分区上。脚本如第 3.3 节所示，使用与上一个脚本相同的分区文件并接受相同的参数。

## 列表 3.3 osinst 安装脚本

```perl
#!/usr/bin/perl

use Getopt::Std;
use Net::Ping;

# Parse the argument list.

$USAGE = "Usage: osinst -t host -p pfile -b bdev\n" . " or osinst -h\n\n" . " -t host    host to install the operating system on\n" . " -p pfile   name of file containing partition information\n" . " -b bdev    device name of boot drive\n" . " -h         print this usage statement\n";

# Parse the arguments
getopts('t:p:b:h');

# Give the usage statement if the ask for it
if (defined $opt_h) {
    print $USAGE;
    exit 1;
}

# Print a usage statement if required arguments are missing
if ((!defined $opt_t) || (!defined $opt_p) || (!defined $opt_b)) {
    print "No target, partition file or boot device specified.\n";
    print $USAGE;
    exit 1;
}

# Check for the existence of the partition file
if ( ! -f $opt_p ) {
    print 'Partition file not found\n';
    print $USAGE;
    exit 1;
}

# Verify that we can reach the target host and if not abort.
if ( ! pingable($opt_t) ) {
    print "Unable to ping target host $opt_t...aborting.\n";
    exit 1;
}

# Next check to see if the boot device exists on the target host.
if ($opt_b =~ /sd/) {
    $avail = `rsh $opt_t 'cat /proc/scsi/scsi' | grep -A2 'Id: 00\*' | grep 'Direct-Access'`;
    chomp $avail;
} else {
    $avail = `rsh $opt_t 'cat /proc/ide/$opt_b/media'`;
    chomp $avail;
    if ($avail ne "disk") {
        $avail = "";
    }
}

if ( $avail eq "" ) {
    print "Unable to verify $opt_b on $opt_t...aborting.\n";
    exit 1;
}

# Now we open the partition definition file, read it one line at a time
# and for each line determine if a mount point is specified and if so,
# mount that partition on the remote system.
open(PFILE, "$opt_p");
while (<PFILE>) {
    ($dnum,$size,$type,$active,$smpt,$smttorder) = split(/,/,$_);
    chomp $smpt;

    if ($smpt ne "") {
        $device = "/dev/sd".$opt_b.$dnum;
        $cmd[$smttorder] = "rsh $opt_t 'mkdir -p /inst/".$smpt."' ; mount $device /inst".$smpt.";";
    }
}

close(PFILE);

for ($i = 1; $i <= scalar @cmd; $i++) {
    print "Executing $cmd[$i]";
    system($cmd[$i]);
}

# Now that the partitions are mounted in the correct order, we can copy
# our template to it.
$tmplt = "/var/lib/OStemplate.afio.gz";
$instcmd = 'cat $tmplt | rsh $opt_t "cd /mnt ; gzip -dc ; afio -i -z /proc/self/fd/0"';

system($instcmd);

exit 0;

################ SUBROUTINES ################

# Check to see if the target host is alive
sub pingable {
    my $target = shift;

    my $p = Net::Ping->new("icmp");
    return $p->ping($target);
}
```

此脚本可以增强以执行诸如检查挂载分区上是否有足够的空间来容纳模板等操作。这留给读者作为练习。

## 对已安装映像进行主机特定自定义

一旦操作系统映像已安装，就需要进行最少的自定义以使系统功能正常。这种自定义包括设置正确的网络设置，特别是 IP 地址和主机名。这可以使用脚本轻松完成，也可以通过登录系统并手动编辑文件来完成。所需的自定义程度取决于多个因素，包括网络的复杂性、是否使用动态 IP 地址分配以及其他因素。如何自定义由您决定。

## 安装引导加载程序

安装不会运行 X Windows 系统的系统的最后一步是安装引导加载程序。这只是针对已安装操作系统映像的一部分的 lilo.conf 文件运行 lilo 的问题。假设您已将已安装的映像挂载为 /mnt，可以通过发出以下命令轻松完成此操作：

```
/mnt/sbin/lilo -r /mnt -v -v
```

完成此操作后，您就可以重新启动新安装的系统。根据您在此过程中添加的自动化程度，您可以使新系统的安装变得简单，只需从软盘启动、连接到网络并从包含操作系统模板的主机发出脚本。我已经使用此方法一段时间，取得了巨大的成功。从软盘启动后安装系统的时间不到五分钟。

这里描述的自制方法只是其中一种方法。如果您不倾向于使用它，还有替代方案，包括来自 Red Hat 的一种方法，称为 kickstart。

## 使用 Kickstart 文件和 RPM

如果前面描述的安装方法听起来工作量很大，那是因为它确实如此。安装多个系统且几乎无需麻烦的一种替代方法是使用 Red Hat 提供的 kickstart 功能。kickstart 方法是通过创建指定安装程序询问的问题的答案的文件来完成的。此文件可以复制到启动软盘上，也可以放在网络上，其名称取决于您选择的这两个选项中的哪一个。有关使用 kickstart 方法的详细信息，请参阅随 Red Hat Linux 软件一起提供的安装指南。使用 kickstart 文件，您可以消除安装程序所需的大部分交互，并预定义要在系统上安装的一组软件包。此方法
