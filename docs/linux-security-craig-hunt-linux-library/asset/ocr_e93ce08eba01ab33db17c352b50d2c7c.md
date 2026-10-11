README doc run src
[ramon]$ cd src
[ramon]$ make
To build John the Ripper, type:

make SYSTEM

where SYSTEM can be one of the following:
linux-x86-any-elf Linux, x86, ELF binaries
linux-x86-mmx-elf Linux, x86 with MMX, ELF binaries
linux-x86-k6-elf Linux, AMD K6, ELF binaries
linux-x86-any-a.out Linux, x86, a.out binaries
linux-alpha Linux, Alpha
linux-sparc Linux, SPARC
generic Any other UNIX system with gcc
[ramon]$ make linux-x86-any-elf
In -sf x86-any.h arch.h

```
make .. /run/john .. /run/unshadow .. /run/unafs .. /run/unique \
JOHN_OBJS="DES_fmt.o DES_std.o BSDI_fmt.o MD5_fmt.o MD5_std.o\ 
BF_fmt.o BF_std.o AFS_fmt.o LM_fmt.o batch.o bench.o charset.o\ 
common.o compiler.o config.o cracker.o external.o formats.o\ 
gotopt.o idle.o inc.o John.o list.o loader.o logger.o math.o\ 
memory.o misc.o options.o params.o path.o recovery.o rpp.o\ 
rules.o signals.o single.o status.o tty.o wordlist.o unshadow.o\ 
unafs.o unique.o x86.o \ \
`CFLAGS="-c -Wall -02 -fomit-frame-pointer -m486"`
make[1]: Entering directory `/home/ramon/john-1.6/src'
gcc -c -Wall -02 -fomit-frame-pointer -m486 -funroll-loops DES_fmt.c
gcc --c - DES_fmt.o DES_std.o BSDI_fmt.o MD5_fmt.o MD5_std.o BF_fmt.o\ 
BF_std.o AFS_fmt.o LM_fmt.o batch.o bench.o charset.o\ 
common.o compiler.o config.o cracker.o external.o formats.o\ 
gotopt.o idle.o inc.o john.o list.o loader.o logger.o math.o\ 
memory.o misc.o options.o params.o path.o recovery.o rpp.o\ 
rules.o signals.o single.o status.o tty.o wordlist.o unshadow.o\ 
unafs.o unique.o x86.o -o .. /run/john
In -s john .. /run/unshadow
In -s john .. /run/unafs
In -s john .. /run/unique
make[1]: Leaving directory `/home/ramon/john-1.6/src'
[ramon]$ ls -1 .. /run/john
-rwxr-xr-x 1 ramon users 148428 Oct 3 19:59 .. /run/john
There is no make installation step, so simply copy the executable to the appropriate place in your filesystem using the following command:

[ramon]$ sudo cp .. /run/john /usr/local/bin
```