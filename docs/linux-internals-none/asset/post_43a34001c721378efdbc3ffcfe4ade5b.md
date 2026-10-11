
## void __init calibrate_delay(void)

```c
void __init calibrate_delay(void)
{
    unsigned long ticks, loopbit;
    int lps_precision = LPS_PREC;

    loops_per_sec = (1<<12);

    printk("Calibrating delay loop... ");
    while (loops_per_sec >>= 1) {
        /* wait for "start of" clock tick */
        ticks = jiffies;
        while (ticks == jiffies)
            /* nothing */;
        /* Go .. */
        ticks = jiffies;
        __delay(loops_per_sec);
        ticks = jiffies - ticks;
        if (ticks)
            break;
    }
}
```

## The lib/ Directory

The lib/ directory holds code that is often needed by other parts of the kernel. For instance, inflate.c can be found here; this code can decompress a kernel at boot and load it into memory. It also knows how to decompress standard PKZIP 8-bit compression algorithms.

## The kernel/ Directory

Some of the most frequently called kernel functions reside in the kernel/ directory. The scheduler, fork(), and timer.c are found here. You will also find printk.c in this directory. Throughout the kernel source code, printk() is used instead of printf(), because the printf() function is not SMP-capable when called from within the kernel. If it were, various tasks running on different CPUs might write to the console or to the syslog at the same time and garble the output.

## The mm/ Directory

The mm/ directory contains the source code to implement the virtual memory manager in the Linux kernel.

## The net/ Directory

All the code for networking support is in the net/ directory. TCP/IP, Netware, and Appletalk are all in here.

## Compiling It

Before you can actually compile the kernel, you must tell the compilation utilities which functionalities you want, and whether to include those functionalities built into the kernel or configured as a dynamically loadable module (we will see later how the kernel handles loadable modules).

Table 2.1 shows the commands used to configure the kernel.

### Table 2.1 Commands used to configure the kernel

| **Type** | **Command (as root)** |
| :------- | :-------------------- |
| Text prompt | `make config` |
| Text menus (ncurses style) | `make menuconfig` |
| GUI (requires X to run) | `make xconfig` |

As you can see in the table above there are three ways to configure a kernel. The `make config` simply opens a character mode dialog that will ask one question after the other on the terminal until all questions are answered. For each question there are three possible answers: Yes, No or Module. Module here tells the kernel configuration to use a loadable module dynamically at execution time instead of statically linking the function into the kernel. This will somewhat slow down the first calling of the particular function at execution time, it is however compensated by a significantly smaller kernel. If you need to fit your kernel onto a diskette this is often the only way to do it.

`make menuconfig` opens up a colourful (on a color terminal) menu-based utility that will allow you to configure the kernel as needed. Most people use to configure their kernels this for the ease of use it offers. The functionality is obviously the same as with the other two commands.

The third way to configure a kernel, is `make xconfig`. This works only if you have a correctly configured and running X Window environment. It will allow to use the mouse to select items and set them as needed.

# Chapter 2

The command `make config` stores your previous choices, so you can always start it again and just change what you need.
Once you have configured your kernel to your satisfaction, you can proceed with the compilation.

```bash
root@maguro /usr/src # make dep; make clean; make bzImage; make modules-install
```

The directive `make bzImage` compiles the kernel and leaves a file in arch/i386/boot called `bzImage` (among other things). The above compilation code might take some time to execute. On a dual PIII 700 MHz with 512MB RAM, this code takes about 4 minutes to run. On a slower computer, compile time will be longer.

Now it's time to install the new kernel. Most people use LILO (the Linux Loader) for this. The command `make bzImage` installs the kernel, runs LILO on it, and gets you all ready to boot, *but only if* LILO is configured in the following way on your system: `kernel` is /vmlinuz, (no, you're right, lilo) is in /sbin, and your `lilo` config (/etc/lilo.conf) agrees with this.

Otherwise, you need to use LILO directly. It's a fairly easy package to install and work with, but it has a tendency to confuse people with its configuration file. Look at the `config` file (either /etc/lilo/config for older versions or /etc/lilo.conf for new versions), to determine the current setup. The config file looks like this:

```text
image = /vmlinuz
  label = Linux
  root = /dev/hda1
...
```

The `image` is is set to the currently installed kernel. Most people use /vmlinuz. The command `label` is used by LILO to determine which kernel or operating system to boot, and `root` is the /directory of that particular operating system.

Make a backup copy of your old kernel and copy the `bzImage` that you just made into place (`cp bzImage /vmlinuz` if you use /vmlinuz).

Rerun LILO. You have now added the kernel to your boot manager. Alternatively, if you wanted to make a boot disk, to check things out before you actually commit your new kernel to the LILO configuration, you could use the `mkbootdisk` utility shipped with most distributions.

## The GNU gcc Compiler

The Linux kernel is written for the GNU gcc compiler. Trying to compile it with any other C compiler will result in complete failure. The source code is full of gcc-specific directives that prevent using anything but the gcc compiler. Because of this gcc affinity, the kernel source code might look strange to people who are used to developing for other C compilers. One such common idiosyncrasy is the use of *inline functions*. An inline function is a directive to the gcc compiler to fully expand the called function in each recurrence, instead of executing a function call each time to a single referenced instance of the called function (which requires expensive stack operations).

Some might object that this precludes achieving truly portable code. This is, however, really not the case. Because the gcc compiler exists on all platforms (inherently so) to which Linux has been ported, the code is portable across those architectures. It is, of course, not portable in the sense of being able to compile correctly under other C compilers. On the other hand, a kernel is not something that requires portability across architectures and compilers. The Linux kernel is optimized for reliability and efficiency, and these two goals are certainly much more important than portability.

## Coding Conventions

After reading this book, you may feel ready to contribute to the Linux kernel. You are obviously welcome to do so, as long as you respect certain conventions.

- Commentaries are always `/* */` style, even for one-line comments. The `//` comment is not acceptable.
- Most often, function-opening brackets (`{`) are on a separate line.
- If statements are coded this way:

```c
if (str[0] >= '0' && str[0] <= '9') {
    strncpy(name, "ttyS");
    strncpy(name + 4, str, sizeof(name) - 5);
} else
    strncpy(name, str, sizeof(name) - 1);
name[sizeof(name) - 1] = 0;
```

- Single-line `if` statements are acceptable:

```c
if (!strcmp(str, "ttya")) strcpy(name, "ttyS");
```

- gotos are quite OK:

- Kernel source, since the earliest times, has always contained a lot of gotos. Linux is no exception. It contains a goto for about every 80 lines of code. This is not because of sloppy programming style, but rather a requirement dictated by the craving for speedy code. In a nested while statement, it is just much easier to use goto to get out of the code rather than break.

## Architecture Dependencies

Linux runs on a wide variety of processor platforms. Almost every month, you can read about a new successful porting to another architecture. Just remember that Linux originated on the i386 processor. This is clearly visible everywhere in the kernel code.

Table 2.2 illustrates the ports achieved so far:

### Table 2.2 Ports achieved so far

| Processor Type | Bit size | Maintainer |
| :------------- | :------- | :--------- |
| Intelx86 | 32 | Linus Torvalds |
| Crusoe | 32 | Linus Torvalds |
| MIPS | 32/64 | Alan Cox |
| IA64 | 64 | The Trillian Project |
| PA-RISC | 64 | The Puffin Group |
| Alpha | 64 | Richard Henderson |
| ARM | 32 | Russell King |
| Sparc | 32/64 | David S. Miller |
| PPC | 32 | Cort Dougan |
| M68000 | 32 | Jes Sorensen |
