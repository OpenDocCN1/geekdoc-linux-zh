author: Joe Thornber
description: device-mapper mirror target
suserlease: openSUSE Leap 15.0
srcversion: A784B8C071D49F47F94E83B
depends: dm-region-hash,dm-mod,dm-log
retpoline: Y
intree: Y
vermagic: [~]SMP mod_unload modversions retpoline
parm: raid1_resync_throttle:A percentage [~]
$


The \texttt{dm\_mirror} module allows volume managers to mirror logical volumes. In Listing 14.8, when the \texttt{modprobe} command is used to load this module, it loads two other modules as well, which the \texttt{dm\_mirror} module needs to work properly. Notice that the \texttt{modprobe} utility is calling the \texttt{insmod} utility to perform the insertion work. Also notice that the \texttt{dm\_mirror} module has a slightly different filename, \texttt{dm-mirror.ko}, shown in the \texttt{modinfo} utility's output.

The \texttt{modprobe} program uses the \texttt{modules.dep} file to determine any module dependencies. This file is typically located in the /lib/modules/ subdirectory, as shown snipped in Listing 14.9.

# **Listing 14.9:** Viewing the \texttt{modules.dep} dependencies file

```
`$ ls /lib/modules/[/]/modules.dep
/lib/modules/[/]/modules.dep
$
$ grep -i mirror /lib/modules/[/]/modules.dep
kernel/drivers/md/dm-mirror.ko:
kernel/drivers/md/dm-region-hash.ko
kernel/drivers/md/dm-log.ko
kernel/drivers/md/dm-mod.ko
$
`
```

In Listing 14.9, the \texttt{modules.dep} file is searched for the word \texttt{mirror} using the \texttt{grep} utility. To see a particular module's dependencies, you locate the module's filename within the file. After the colon (\,:\,) , the module's dependencies are listed by their full module filename. So for the \texttt{dm\_mirror} modules (\texttt{dm-mirror.ko}), the module dependencies are the \texttt{dm-region-hash}, \texttt{dm-log}, and \texttt{dm-mod} modules. This corresponds with what was shown in the \texttt{modinfo} utility's output in Listing 14.8.

You can employ the \texttt{depmod} command to scan through the system looking for any hardware that was not automatically detected. This is useful for troubleshooting problems with new devices. A snipped example is shown in Listing 14.10.