```
rm -f trampoline hexify
make[1]: Leaving directory `/usr/src/linux-2.0.34/arch/i386/kernel'
rm -f kernel/ksyms.lst include/linux/compile.h
rm -f core `find . -name '*.I'` ! -regex '.*lxdiaglog/.*' -print'
rm -f core `find . -type f -name 'core' -print'
rm -f vmlinux System.map
rm .tmp* drivers/sound/configure
rm -fr modules/*
rm -f submenu*
```

If everything goes smoothly (and it should), run `make zImage`. This will install a new kernel in `/usr/src/linux/arch/i386/boot`. The file will be called `zImage`.

> When you're compiling the kernel, you may find that time is standing still. You may want to get a few cups of coffee or read the paper while you're kernel is recompiling. How long does it take? It depends on the size of your kernel, the speed of your processor, and what else you're running. The smaller the kernel, the faster it will compile. The faster your process, the faster it will compile. If you're not running other intensive applications (such as X), it will compile faster.

If you added lots of drivers or support to your kernel, you may want to use `make bzImage`, as shown in Listing 6-14. This enables you to make a big image that can boot with all your options. I've included a small section of what you may see while you are creating the new kernel.

```
# make zImage
make[1]: Entering directory `/usr/src/linux-2.0.30/arch/i386/boot'
make[1]: Nothing to be done for `dep'.
make[1]: Leaving directory `/usr/src/linux-2.0.30/arch/i386/boot'
scripts/mkdep int/* .c .tmpdepend
scripts/mkdep `find /usr/src/linux/include/asm /usr/src/linux/include/linux
/usr/src/linux/include/scsi /usr/src/linux/include/net -follow -name \.h !
-name modversions.h -print` > .hdepend
set -e; for i in kernel drivers mm fs net ipc lib arch/i386/kernel
arch/i386/mm
arch/i386/lib; do make -C $i fastdep; done
ld -m elf_i386 .-r -o mmo init.o fault.o
```