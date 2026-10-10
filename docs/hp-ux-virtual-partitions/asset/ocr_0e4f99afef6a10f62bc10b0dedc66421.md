![](bbox=[0.045, 0.05, 0.105, 0.148])

vparboot - Boots (starts) a virtual partition.

vparboot (1M)

NAME
vparboot - boot a virtual partition

SYNOPSIS
vparboot -p vp_name [-b kernel_path] [-o boot_opts] [-B boot_addr]
vparboot -p vp_name -i ignite_kernel

DESCRIPTION
The vparboot command causes the virtual partition monitor to boot the specified virtual partition. The monitor must be running. The virtual partition must exist in the monitor configuration and be in the Down state. For example, not running. For this reason, it is not possible to boot the current partition using this command. The partition in which the command is executing is called the current partition.

Only a superuser can execute the vparboot command.

Options
'vparboot' recognizes the following command line options and arguments:

-p vp_name
Specifies the unique name of the virtual partition which is to be booted. The virtual partition must exist in the monitor's database, must be in the Down state, and must have a configured boot device. Required.

-b kernel_path
Specifies the absolute path to a bootable kernel for the virtual partition. For example, if a non-partitioned system start string at the ISL prompt is:
ISL> hpx -is /stand/vmunix
the kernel-path is the /stand/vmunix portion of this string.

If this option is omitted, the value is taken from any -b kernel_path specified during virtual partition creation or its most recent modification, or /stand/vmunix if -b kernel_path has never been specified.

-o boot_opts
Specifies the command-line options applied when the virtual partition is booted. For example, if a non-partitioned system start string at the ISL prompt is: