On SUSE Linux Enterprise Server 10, depmod also creates the file modules.aliases, which is used by hwup and modprobe to determine which driver needs to be loaded for which device. Learn more about this file in the hwup objective in this section.

+   - **modinfo option module.** This command displays information (such as license, author, and description) about the module indicated on the command line.

The following is an example:

```
DAS0:~ # modinfo isdn
license:        GPL
author:         Fritz Elfert
description:    ISDN4Linux: link layer
depends:        slhc
supported:      yes
vermagic:       2.6.5-7.21-default 586 REGPARM gcc-3.3
```

For more detailed information, enter **man modinfo**.