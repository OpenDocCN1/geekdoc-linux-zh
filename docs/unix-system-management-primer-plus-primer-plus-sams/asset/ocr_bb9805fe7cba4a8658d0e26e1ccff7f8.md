# Chapter 7 • PATCHES, UPGRADES, AND DECOMMISIONS

Patch-ID# 108984-07
Keywords: QLC ISP2200 buffer PCI FiberChannel FCode CPR PM
Synopsis: SunOS 5.8: qlc patch
Date: 21/Jan/01

Solaris Release: 8

SunOS release: 5.8

Unbundled Product:

Unbundled Release:

Topic: SunOS 5.8: qlc patch

NOTE: Refer to Special Install Instructions section for
IMPORTANT specific information on this patch.

BugID-fixed with this patch: 426423 427254 430040 430943 430953 432087 4
304897 431982 432426 432419 432447 432689 432791 432844 433070 4
334839 435949 433664 433665 433667 436678 434485 435485 435397 435386 4
335815 435831 435385 435529 437594 436806 436051 436023 436312 436458 4
366910 436742 436950 437520 437754 437765 438079

Changes incorporated in this version: 438079

Relevant Architectures: sparc

Patches accumulated and obsoleted by this patch: 110190-01

Patches which conflict with this patch:

Patches required with this patch:

Obsolete by:

Files included with this patch:

```
/etc/driver_aliases
/etc/driver_classes
/etc/name_to_major
/kernel/drv/qlc
/kernel/drv/qlc.conf
/kernel/drv/sparc9/qlc
[remainder of file truncated]
```

This README text clearly explains what the patch does and the files it replaces (including
/kernel/drv/qlc.conf). You must make sure that your prepatch backup includes all of the
files that will be changed by the patch application. After the patching process is complete,
y can replace the rewritten config file with the original.