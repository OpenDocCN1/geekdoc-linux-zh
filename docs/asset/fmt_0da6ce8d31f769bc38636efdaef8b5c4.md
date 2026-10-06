
内存映射 `/dev/zero` 是一种分配内存的高级技术。更多信息请参阅第 5 章“进程间通信”中的第 5.3.5 节“`mmap` 的其他用途”，示例请参阅第 8 章“Linux 系统调用”中的第 8.9 节“`mprotect`: 设置内存权限”中的侧边栏“获取页对齐内存”。

### 6.5.3 /dev/full

条目 `/dev/full` 的行为就像文件系统上一个已经没有剩余空间的文件。向 `/dev/full` 写入数据将失败，并将 `errno` 设置为 `ENOSPC`，这通常表示被写入的设备已满。

例如，你可以尝试使用 `cp` 命令向 `/dev/full` 写入：

```
% cp /etc/fstab /dev/full
cp /dev/full: No space left on device
```

`/dev/full` 条目主要用于测试当你的程序在写入文件时磁盘空间耗尽时的表现。

### 6.5.4 随机数设备

特殊设备 `/dev/random` 和 `/dev/urandom` 提供了对 Linux 内核内置随机数生成器的访问。

大多数生成随机数的函数（例如标准 C 库中的 `rand` 函数）实际上生成的是伪随机数。尽管这些数满足随机数的某些属性，但它们是可重复的：如果你从相同的种子值开始，每次都会获得相同的伪随机数序列。这种行为是不希望的，因为计算机在本质上是确定且可预测的。然而，对于某些应用程序来说，这种行为是不可接受的；例如，如果你能获取加密算法所使用的随机数序列，有时就可以破解该算法。

要在计算机程序中获得更好的数字，需要外部随机性源。Linux 内核收集了一个特别好的随机性源；通过测量你的输入动作（如击键和鼠标移动）之间的时间延迟，Linux 能够生成不可预测的高质量随机数流。你可以通过读取 `/dev/random` 和 `/dev/urandom` 来访问它。你读取的数据是随机生成的字节。

当 Linux 耗尽其随机性存储时，这两个设备之间的区别在于：如果你尝试从 `/dev/random` 读取大量字节但不产生任何输入动作（你不打字、不移动鼠标或执行类似的操作），Linux 会阻塞读取操作。只有当你提供了一些随机性时，Linux 才会生成更多的随机字节并将它们返回给你的程序。

例如，尝试使用 `od` 命令显示 `/dev/random` 的内容。输出的每行显示 16 个随机字节。

- 我们使用 `od` 而不是列表 B.4 所示的 `hexdump` 程序，尽管我们要做相同的事情，因为 `hexdump` 在数据耗尽时会终止，而 `od` 会等待更多数据可用。`-t x` 告诉 `od` 以十六进制格式打印文件内容。

```
% od -t1 /dev/random
0000000 2c 9c 7a 2b 2e 79 35 36 c2 e3 1b 52 75
0000010 61 7d 7d 5d 7d 5d 7d 5d 5d 7d 1d 7d
00000020 5d 1d 7d 5d 5d 1d 7d 1d 1d 1d 7d 7d
00000030 7d 1d 7d 7d 5d 1d 1d 7d 7d 1d 1d 7d
```

## 140 第 6 章 设备

要构建虚拟文件系统并使用回环设备将其挂载，请遵循以下步骤：

- 1. 创建一个空文件来存放虚拟文件系统。该文件的大小即为回环设备挂载后的显示大小。

  使用 `dd` 命令构建固定大小文件的一种方法。该命令从一个文件复制块到另一个文件（默认每个块512 字节）。`/dev/zero` 文件是一个方便的字节拷贝源。

  要创建一个名为 `disk-image` 的 10MB 文件，请调用以下：

```bash
dd if=/dev/zero out=/tmp/disk-image count=20480
20480+ records in
20480+ records out
ls -l /tmp/disk-image
-rw-r--r-- 1 root 10485760 Mar 8 01:56 /tmp/disk-image
```

- 2. 你创建的文件充满了 0 字节。在挂载它之前，你必须构建并存储文件，并建立根目录以组织所需的各种控制结构。

  你可以在磁盘镜像中构建任何你喜欢的文件系统。要构建一个 ext2 文件系统（Linux 磁盘最常用的类型），请使用 `mke2fs` 命令。因为它通常运行在块设备而非普通文件上，所以会请求确认：

```bash
mke2fs -q /tmp/disk-image
mke2fs 1.18, 11-Nov-1999 EXT2 FS 0.5b, 95/08/09
disk-image is not a block special device.
Proceed anyway? (y,n)
```

  `-q` 选项抑制关于新创建文件系统的摘要信息。如果你对此感兴趣，请省略此选项。

  现在 `disk-image` 包含了一个全新的文件系统，就像一个刚初始的 10MB 磁盘驱动器。

## 6.5 特殊设备 141

例如，要挂载你的 `disk-image` 文件系统，请调用这些命令。记住，只有超级用户可以使用回环设备。第一条命令创建一个目录 `/tmp/virtual-fs` 作为虚拟文件系统的挂载点。

```
% mkdir /tmp/virtual-fs
% mount -o loop=/dev/loop0 /tmp/disk-image /tmp/virtual-fs
```

现在，你的磁盘镜像已经挂载，就像一个普通的 10MB 磁盘驱动器。

```
df -h /tmp/virtual-fs
Filesystem Size Used Avail Mounted on
/tmp/disk-image 9.7M 13k 9.2M 0% /tmp/virtual-fs
```

你可以像使用其他磁盘一样使用它：

```
% cd /tmp/virtual-fs
% echo 'Hello, world!' > test.txt
% ls -l
total 13
drwxr-xr-x 2 root root 12288 Mar 8 02:00 lost+found
-rw-r--r-- 1 root root 14 Mar 8 02:12 test.txt
% cat test.txt
Hello, world!
```

注意，`lost+found` 是由 `mkfs.3` 自动添加的目录。

- 5. 如果文件系统发生损坏，并且恢复了一些数据但未与文件关联，则它们会被放在 `lost+found` 中。

## 142 第 6 章 设备

完成后，请卸载虚拟文件系统。

```
% cd /tmp
% umount /tmp/virtual-fs
```

你可以根据需要删除 `disk-image`，或者在稍后挂载它以访问虚拟文件系统上的文件。你也可以将其复制到另一台计算机并挂载——你创建的整个文件系统将保持完好。

与其从零开始创建文件系统，不如直接从设备复制一个。例如，你只需通过从 CD-ROM 设备复制，即可创建 CD-ROM 内容的内容。

如果你有一个 IDE CD-ROM 驱动器，使用之前描述的相应设备名称，例如 `/dev/hda`。如果你有一个 SCSI CD-ROM 驱动器，设备名称将为 `/dev/scd0` 或类似。你的系统可能有一个符号链接 `/dev/fstab` 来确定哪个设备对应于计算机的 CD-ROM 驱动器。

只需将设备复制到文件。生成的文件将是 CD-ROM 上文件系统的完整镜像——例如：

```
% cp /dev/cdrom /tmp/cdrom-image
```

这可能需要几分钟，取决于你正在复制的 CD-ROM 以及你的驱动器速度。生成的镜像将很大——与 CD-ROM 的内容一样大。

现在你可以在没有原始 CD-ROM 驱动器的情况下挂载此 CD-ROM 镜像。例如，将其挂载到 `/mnt/cdrom`，使用此行：

```
% mount -o loop=/dev/loop0 /tmp/cdrom-image /mnt/cdrom
```

由于镜像是一个硬盘驱动器，它的运行速度会比实际的 CD-ROM 磁盘快得多。大多数 CD-ROM 使用 iso9660 文件系统。

### 6.6 PTYs

如果你带有命令行参数运行 `mount` 命令以显示文件系统，[源文本似乎出现重复/损坏]。

列表 6.2 展示了一个短程序，用于弹出 CD-ROM 驱动器的磁盘（如果驱动器支持此操作）。它接受一个命令行参数，即 CD-ROM 驱动器设备。它打开指向该设备的文件描述符，并带有请求代码 `CROMEJECT` 调用 `ioctl`。该请求定义在头文件 `<linux/cdrom.h>` 中，指示设备弹出磁盘。

例如，如果你的系统有一个 IDE CD-ROM 驱动器作为主设备连接在次级 IDE 控制器上，那么对应的设备设备是 `/dev/hdc`。要从次级 IDE 控制器弹出磁盘，请执行此行命令：

```bash
% ./cdrom-eject /dev/hdc
```

## 7 /proc 文件系统

尝试在不带参数的情况下调用 `mount` 命令——这会显示当前挂载在你的 GNU/Linux 计算机上的文件系统。你会看到类似下面的一行：

```
none on /proc type proc (rw)
```

这就是特殊的 `/proc` 文件系统。注意，第一个文件 `none` 表示该文件系统与磁盘驱动器等硬件设备无关。相反，`/proc` 是通往运行中的 Linux 内核的窗口。`/proc` 文件系统中的文件并不对应物理设备上的实际文件。相反，它们是魔法对象，行为像文件，但提供了对内核中参数、数据结构和统计信息的访问。这些文件的“内容”并不总是固定数据块（像普通文件内容那样）。相反，它们是你从文件中读取时由 Linux 内核动态生成的。你还可以通过向 `/proc` 文件系统中的文件写入内容来更改运行内核的配置。

让我们看这个示例：

```
ls -l /proc/version root 0 Jan 17 18:09 /proc/version
```

注意文件大小为 0；因为文件内容是由内核生成的，所以文件大小的概念在这里并不适用。此外，如果你亲自尝试此命令，你会发现文件的修改时间是当前时间。

这个文件里包含什么？`/proc/version` 的内容由一个描述内核版本号的字符串组成。它包含了通过 `uname` 系统调用获取的版本信息（这在第 8 章“Linux 系统调用”的第 8.15 节“`uname`”中描述），以及附加信息，例如用于编译内核的编译器版本。你可以像读取任何其他文件一样读取 `/proc/version`。使用 `cat` 命令可以方便地显示其内容。

```
% cat /proc/version
Linux version 2.2.14-58.0 (root@porky.devel.redhat.com) (gcc egcs-2.91
66 19990314/Linux (egcs-1.1.2 release)) Tue Mar 27 21:07:39 EST 2000
```

`/proc` 文件系统中的项目在 man 手页（第 5 节）中有详细描述。要查看它，请执行此命令：

- `man 5 proc`

在本章中，我们将描述 `/proc` 文件系统中可能对应用程序程序员最有用的特性，并提供使用它们的示例。`/proc` 的某些特性对于调试也很有帮助。

如果你对 `/proc` 的工作原理感兴趣，可以查看 Linux 内核的源码，位于 `/usr/src/linux/fs/proc/`。

### 7.1 从 /proc 中提取信息

`/proc` 中的大多数条目都提供了了人类可读格式的信息，但这些格式足够简单，可以于解析。例如，`/proc/cpuinfo` 包含了关于系统 CPU（对于多处理器机器，则多个 CPU）的信息。输出是一个值表，每行一个，每个值都有一个描述，并在每个值前面有一个冒号。

例如，输出可能如下：

```
% cat /proc/cpuinfo
processor : 0
vendor_id : GenuineIntel
cpu family : 6
model : 5
model name : Pentium II (Desutches)
stepping : 2
cpu MHz : 400.913520
cache size : 512 KB
fdiv_bug : no
hlt_bug : no
sep_bug : no
f00f_bug : no,coma_bug : no
fpu : yes
fpu_exception : yes
cpuid level : 2
flags : yes
wp : fpu vme de pse tsc msr pae cxe8 apic fxsr
mtr pga cmov mov pse36 mmx fxsr
bogomips : 399.77
```

我们将在第 7.3.1 节“CPU 信息”中描述这些字段的含义。

从此输出中提取值的简单方法是将文件读取到缓冲区并在内存中使用 `sscanf` 进行解析。7.1 显示了此方法的示例。该程序包含了 `get_cpu_clock_speed` 函数，它从 `/proc/cpuinfo` 读取到内存并提取第一个 CPU 速度。

列表 7.1 (`clock-speed.c`) 从 `/proc/cpuinfo` 提取 CPU 速度

```c
#include <stdio.h>
#include <string.h>

/* 返回第一个 CPU 的时钟频率。出错时返回。 */
float get_cpu_clock_speed() {
    FILE *fp;
    char buffer[1024];
    size_t bytes_read;
    char *match;
    float clock_speed;

    /* 将 /proc/cpuinfo 的全部内容读入缓冲区 */
    fp = fopen("/proc/cpuinfo", "r");
    bytes_read = fread(buffer, 1, sizeof(buffer) - 1, fp);
    fclose(fp);
    /* 如果读取失败或缓冲区不足，返回 0。（注意：简化版） */
    buffer[bytes_read] = '\0';
    /* 找到以 "cpu MHz" 开头的行 */
    match = strstr(buffer, "cpu MHz");
    if (match == NULL)
        return 0;
    /* 解析行以提取速度 */
    sscanf(match, "cpu MHz: %f", &clock_speed);
    return clock_speed;
}

int main() {
    printf("CPU speed: %.4f MHz\n", get_cpu_clock_speed());
    return 0;
}
```

但请注意，proc 文件系统中项目的名称、语义和输出格式会在内核更新中发生变化。如果你在 proc 条目中使用它们，应确保程序在条目缺失或格式异常时能够优雅处理。

### 7.2 进程目录

`/proc` 文件系统为 GNU/Linux 系统上运行的每个进程一个目录。每个目录的名称是对应进程的进程 ID。这些目录随着进程的启动和终止而动态出现和消失。每个目录包含多个关于运行中进程的项目。proc 文件通过这些进程目录进行命名。

- `cmdline` 包含进程的参数列表。`cmdline` 条目在第 7.2.2 节“进程参数列表”中描述。

- `cwd` 是指向当前工作目录的符号链接（例如通过 `chroot` 调用设置）。

- `environ` 包含进程的环境。`environ` 条目在第 7.2.3 节“进程环境”中描述。

- `exe` 是指向进程运行的可执行映像的符号链接。`exe` 条目在第 7.2.4 节“进程执行文件”中描述。

- `fd` 是子目录，包含进程打开的文件描述符的项目。这些项目在第 7.2.5 节“进程文件描述符”中描述。

- `maps` 显示映射到进程地址的文件的信息。详见第 5 章“进程间通信”第 5.3 节“映射内存”。对于每个映射的文件，`maps` 显示了文件被映射到进程地址空间的地址范围、这些地址的权限、文件名以及其他信息。

`maps` 表为每个进程显示了运行中的程序、任何加载的共享库以及进程映射的其他文件。

- `root` 是指向该进程根目录的符号链接。通常，它是指向 `/`（系统根目录）的符号链接。进程的根目录可以使用 `chroot` 调用或 `chroot` 命令进行更改。

## 7.2 进程项 151

- `stat` 包含了大量关于进程的状态和统计信息。这些数据与 `status` 条目提供的数据相同，但以原始数值格式呈现，且位于同一行。这种格式难以阅读，但可能更适合解析程序。

- 如果你想在程序中使用 `stat`，请查看 `proc` 手册页，它通过调用 `man 5 proc` 来描述其内容。

- `statm` 包含了关于进程使用内存的信息。`statm` 条目的描述在第 7.2.6 节“进程内存统计”中。

- `status` 包含了大量关于进程的状态和统计信息，格式化后便于人类理解。第 7.2.7 节“进程统计”包含了对 `status` 条目的描述。

- `cstat` 仅在 SMP Linux 内核上出现。它包含了按 CPU 分类的进程时间（用户态和内核态）。

出于安全考虑，某些条目的权限被设置为只有拥有该进程的用户（或超级用户）才能访问它们。

#### 7.2.1 /proc/self

`/proc` 文件系统中的一个条目使得通过 `/proc` 查找当前进程的信息变得简单。`/proc/self` 是一个指向当前进程对应的 `/proc` 目录的符号链接。`/proc/self` 链接的目标取决于哪个进程在查看它；每个进程都将自己的进程目录作为链接的目标。
