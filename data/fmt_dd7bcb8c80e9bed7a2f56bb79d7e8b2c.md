
`modprobe` 工具由一个名为 `modprobe.conf` 的配置文件驱动。这允许系统开发者将设备与设备驱动关联起来。对于简单的嵌入式系统，`modprobe.conf` 可能是空的或包含极少数行。`modprobe` 工具编译时包含了一组默认规则，在缺少有效 `modprobe.conf` 的情况下建立默认设置。仅使用 `-c` 选项调用 `modprobe` 可以显示 `modprobe` 使用的默认规则。

列表 8-8 显示了一个典型的 `modprobe.conf`，它可能出现在包含两个以太接口的系统中。其中一个是基于 Prism2 芯片的无线适配器，另一个是典型的 PCI 以太卡。该系统还包含一个基于集成 Intel 音频芯片的声音子系统。

### 列表 8-8 典型的 modprobe.conf 文件

```bash
$ cat /etc/modprobe.conf

alias eth1 orinocno_pci

options eth1 orinocno_debug=9

alias eth0 e100

alias snd-card-0 snd-intel8x0

options snd-card-0 index=0

$
```

当内核启动并发现无线芯片时，该文件指示 `modprobe` 加载 `orinocno_pci` 设备驱动，该驱动绑定到内核设备 `eth1`。然后它将可选的模块参数 `orinocno_debug=9` 传递给驱动。发现声卡硬件时也会执行相同的操作。注意与声音驱动 `snd-intel8x0` 关联的可选参数。

注意，`modprobe.conf` 的功能在很大程度上已被 `udev` 的功能取代。这将在第 19 章中介绍。然而，你可能会在旧的嵌入式系统中发现 `modprobe.conf`，因此了解如何配置它可能会有所帮助。

## 8.2.4 depmod

`modprobe` 如何知道给定模块的依赖关系？`depmod` 工具在此过程中起着关键作用。当执行 `modprobe` 时，它会在模块安装的相同目录下搜索一个名为 `modules.dep` 的文件。`depmod` 工具会创建这个模块依赖文件。

该文件包含了内核构建系统已配置的所有模块列表，以及每个模块的依赖信息。这是一种简单的格式，每个设备模块占用文件中的一行。如果模块有依赖关系，它们将按顺序列在模块名称之后。例如，在列表 8-7 中，我们看到 `ext3` 模块对 `jbd` 模块有依赖。`modules.dep` 中的依赖行看起来如下：

```
ext3.ko: jbd.ko
```

在实际操作中，每个模块名称之前都有其在文件系统中的绝对路径以避免歧义。为了可读性，我们省略了路径信息。更复杂的依赖链（例如声音驱动）可能像这样：

```
snd-intel80.ko snd-ac97-codec.ko snd-pcm.ko snd-timer.ko \
snd.ko soundcore.ko snd-page-alloc.ko
```

同样，为了可读性我们删除了路径部分。`modules.dep` 文件中的每个模块文件名都是绝对文件名，具有完整的路径信息，并存在于单行中。之前的示例为了适应页面宽度被分成了两行。

通常，`depmod` 在内核构建期间自动运行。然而，在交叉开发环境中，你必须有一个核心版本的 `depmod`，它能够读取以你目标架构原生格式编译的模块。或者，大多数嵌入式发行版都有方法和初始化脚本条目，在每次启动时运行 `depmod`，以确保模块依赖关系是最新的。

## 8.2.5 rmmod

`rmmod` 工具也很简单。它只是从运行中的内核中移除模块。将模块名作为参数传递给它。不需要包含路径或文件扩展。例如：

```bash
# rmmod hellol <<< 必须是 root
```

这里唯一值得理解的点是，当你使用 `rmmod` 时，它会执行模块的 `*exit()*` 函数，正如我们在列表 8-1 和 8-6 的 `hellol.c` 示例所示。

应该注意的是，与 `modprobe` 不同，`rmmod` 不要求依赖模块。请使用 `modprobe -r` 执行此操作。

## 8.2.6 modinfo

你可能注意到了列表 8-6 中骨架驱动的最后三行。这些宏的作用是在二进制模块中放置标签，以便于其管理和配置。列表 8-9 是对我们的 `hellol.ko` 模块执行 `modinfo` 的结果。

### 列表 8-9 modinfo 输出

```text
$ modinfo hellol

filename:      /lib/modules/../kernel/drivers/char/examples/hellol.ko

license:      GPL

description:  Hello World Example

author:       Chris Hallinan

depends:

vermagic:     2.6.32-0750-g8bea867 mod_load modversions ARMv5

arm:          debug_enable:Enable module debug mode. (int)
```

第一个字段显而易见：它是设备驱动模块的完整文件名。为了可读性，我们再次截断了路径。接几行是列表 8-6 结尾描述宏的直接结果——文件名、作者和许可证信息。这些仅仅是模块工具的标签；它们不会影响设备驱动插入的行为。你可以了解更多关于这些工具的信息。

# 列表 8-10 继续

```c
/* 在此处进行初始化... */

return 0;

hello_fail:

    return ret;

}

static void __exit hello_exit(void)

{

    printk("Hello Example Exit\n");

}

struct file_operations hello_fops = {

    owner: THIS_MODULE,

    read: hello_read,

    write: hello_write,

    ioctl: hello_ioctl,

    open: hello_open,

    release: hello_release,

};

module_init(hello_init);

module_exit(hello_exit);
```
