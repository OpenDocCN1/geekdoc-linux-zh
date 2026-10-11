```
make[2]: Leaving directory `/usr/src/linux-2.0.30/arch/i386/mm`
make[1]: Leaving directory `/usr/src/linux-2.0.30/arch/i386/mm`
make[1]: Entering directory `/usr/src/linux-2.0.30/arch/i386/lib`

make all_targets

make[2]: Entering directory `/usr/src/linux-2.0.30/arch/i386/lib`
gcc -D__KERNEL__ -I/usr/src/linux/include -Wall -Wstrict-prototypes -O2 -fomit-
frame-pointer -fno-strength-reduce -pipe -m486 -malign-loops=2 -malign-jumps=2
-malign-functions=2 -DCPU=586 -c -o checksum.o checksum.c
gcc -D__KERNEL__ -I/usr/src/linux/include -D__ASSEMBLY__ -traditional -c
semaphore.S -o semaphore.o
rm -f lib.a
ar rcs lib.a checksum.o semaphore.o
make[2]: Leaving directory `/usr/src/linux-2.0.30/arch/i386/lib`
make[1]: Leaving directory `/usr/src/linux-2.0.30/arch/i386/lib`
ld -m elf_i386 -Ttext 0x100000 -e text arch/i386/kernel/head.o init/main.o
init/version.o \
..arch/i386/kernel/kernel.o arch/i386/mm/mm.o kernel/kernel.o mm/mm.o fs/fs.o
ipc/ipc.o net/network.o \
..fs/file_systems.a \
make[2]: Entering directory `/usr/src/linux-2.0.30/arch/i386/boot/compressed`
tmppiggy=$tmp/$piggy; \\
rm -f $tmp/piggy $tmp/piggy.gz $tmp/piggy.lnk; \\
if hash encas 2>/dev/null; then \\
obdump -k -q. -o 0x100000 /usr/src/linux/vmlinux > $tmp/piggy; \\
else \\
objcopy -O binary -R .note -R .comment -R .stab -R .stabstr
/usr/src/linux/vmlinux $tmp/piggy; \\
fi; \\
gzip -f -9 < $tmp/piggy > $tmp/piggy.gz; \\
if hash encas 2>/dev/null; then \\
encas -target elf32-i386 piggy.o $tmp/piggy.gz input_data input_len; \\
else \\
echo "SECTIONS { .data : { input_len = .; LONG(input_data_end - input_data)
input_data = .; *(.data) input_data_end = .; }}" > $tmp/piggy.lnk; \\
ld -m elf_i386 -m elf_i386 -r -o piggy.o -b binary $tmp/piggy.gz -b elf32-i386
-T $tmp/piggy.lnk; \\
fi;
rm -f $tmp/piggy $tmp/piggy.gz $tmp/piggy.lnk
gcc -D__KERNEL__ -I/usr/src/linux/include -traditional -c head.S
gcc -D__KERNEL__ -I/usr/src/linux/include -O2 -DSTDC_HEADERS -c misc.c -o
misc.o
```