
ally 运行一个脚本来设置它。对于以太网卡来说尤其方便——插入卡后，脚本可以运行适当的 ifconfig 和 route 命令，使其立即工作。

## PROBLEM 88

Symptom: 你收到错误信息 .. symbols don’t match version.
Problem: 你存在内核模块不匹配的问题。
Fix: 你需要使用当前内核的 include 文件重新编译此模块。事先确保 /usr/include/linux 和 /usr/include/asm 指向当前源树中的位置。

## PROBLEM 89

Symptom: 你收到错误信息 module.o: unresolved symbol symname.
Problem: 你在尝试使用 insmod 时没有加载依赖项。
Fix: 找到具有 symname 的模块。如果它可用，请查看 /lib/modules/version/modules.dep 是否列出了 module.o；这将显示 depmod -a 找到的依赖项。如果所有内容都正确，你可以使用 modprobe 来加载依赖项和模块。

## 7.6 Troubleshooting

对当前运行的内核进行一般检查的最佳方法之一是使用 /proc 文件系统。这里面的许多文件包含与配置相关的参数和列表，但有些文件并不像你想象的那样工作。

### /proc/filesystems

如果你运行 cat /proc/filesystems，你将获得内核已知的[content]
ally 运行一个脚本来设置它。对于以太网卡来说尤其方便——插入卡后，脚本可以运行适当的 ifconfig 和 route 命令，使其立即工作。

## PROBLEM 88

Symptom: 你收到错误信息 .. symbols don’t match version.
Problem: 你存在内核模块不匹配的问题。
Fix: 你需要使用当前内核的 include 文件重新编译此模块。事先确保 /usr/include/linux 和 /usr/include/asm 指向当前源树中的位置。

## PROBLEM 89

Symptom: 你收到错误信息 module.o: unresolved symbol symname.
Problem: 你在尝试使用 insmod 时没有加载依赖项。
Fix: 找到具有 symname 的模块。如果它可用，请查看 /lib/modules/version/modules.dep 是否列出了 module.o；这将显示 depmod -a 找到的依赖项。如果所有内容都正确，你可以使用 modprobe 来加载依赖项和模块。

## 7.6 Troubleshooting

对当前运行的内核进行一般检查的最佳方法之一是使用 /proc 文件系统。这里面的许多文件包含与配置相关的参数和列表，但有些文件并不像你想象的那样工作。

### /proc/filesystems

如果你运行 cat /proc/filesystems，你将获得内核已知的[content]
ally 运行一个脚本来设置它。对于以太网卡来说尤其方便——插入卡后，脚本可以运行适当的 ifconfig 和 route 命令，使其立即工作。

## PROBLEM 88

Symptom: 你收到错误信息 .. symbols don’t match version.
Problem: 你存在内核模块不匹配的问题。
Fix: 你需要使用当前内核的 include 文件重新编译此模块。事先确保 /usr/include/linux 和 /usr/include/asm 指向当前源树中的位置。

## PROBLEM 89

Symptom: 你收到错误信息 module.o: unresolved symbol symname.
Problem: 你在尝试使用 insmod 时没有加载依赖项。
Fix: 找到具有 symname 的模块。如果它可用，请查看 /lib/modules/version/modules.dep 是否列出了 module.o；这将显示 depmod -a 找到的依赖项。如果所有内容都正确，你可以使用 modprobe 来加载依赖项和模块。

## 7.6 Troubleshooting

对当前运行的内核进行一般检查的最佳方法之一是使用 /proc 文件系统。这里面的许多文件包含与配置相关的参数和列表，但有些文件并不像你想象的那样工作。

### /proc/filesystems

如果你运行 cat /proc/filesystems，你将获得内核已知的
