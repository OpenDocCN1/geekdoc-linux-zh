```
CONFIG_CONFIGLANG_ENGLISH=y
# CONFIG_CONFIGLANG_GERMAN is not set
#
# Code maturity level options
#
# CONFIG_EXPERIMENTAL is not set
#
# Processor type and features
#
# CONFIG_M386 is not set
# CONFIG_M486 is not set
CONFIG_M586=y
# CONFIG_M586TSC is not set
# CONFIG_M686 is not set
CONFIG_X86_WP_WORKS_OK=y
CONFIG_X86_INVLPG=y
CONFIG_X86_BSWAP=y
CONFIG_X86_POPAD_OK=y
CONFIG_MATH_EMULATION=y
CONFIG_MTRR=y
# CONFIG_SMP is not set
```

As you can see, the file is very simple to understand. Although it says at the beginning of the file not to attempt to edit it, if you know what you are doing, you can go ahead and edit the file yourself. There is little need to edit it yourself, but sometimes if you just want to turn on or off one option, it can be faster to just do it by editing that file manually rather than loading one of the configuration utilities. But, just in case, back up that file before attempting to tamper with it manually—better safe than sorry.

# Troubleshooting

There are a few common problems that can occur when compiling the kernel. The following is a short list of these, along with suggested remedies:

*When I run make bzImage, it says something about the image being too big or something like that.*

This is a fairly common error, specifically with the 2.2.x series of kernels. This is usually caused by having a lot of the options built in the kernel and not having them as modules. Built-in options increase the size of the kernel; so it is better to have most of the options as modules because this keeps the kernel small. So go through your kernel's configuration and see which options you can set as modules—the more the better.

*The kernel acts weird (crashes, exhibits I/O problems).*

This is usually caused by forgetting to run a make clean and make dep command. Running them and recompiling usually solves the problem. Another cause for this could be the version of the compiler that you are using to compile the kernel. SuSE comes with the appropriate