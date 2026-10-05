# SuSE System Administration
PART III

# TABLE 24.2 Ghostscript Drivers and Supported Printers

| Driver | Printer(s) |
| --- | --- |
| unprint | Canon BJC 610, HP DeskJet 550C, NEC P2X, Epson Stylus Color, II, 500, 600, 1520 |
| xes | Xerox XES 2700, 3700, 4045 |

In general, if you have a printer that supports some form of printer control language (PCL), you shouldn't have problems.

> Note
Don't be dismayed if you do not find a driver that exactly matches your printer. Many drivers are compatible with a range of printers, and you may discover that your printer is supported by one of the included drivers. For example, Canon BJC 50 users will find support with the BJC 600 drivers, and HP 340 users can print using the HP 500 drivers.

# How Do I Print?

First, check first to see that your printer is plugged in, turned on, and attached to your computer's parallel port. Pass-through parallel port cables shouldn't pose a problem.

For starters, try this simple code (as root):

```
# ls /dev/lp0
```

Chances are your printer will activate and its print head move. When you look at the printout, you might see a staircase effect, with each word on a separate line, moving across the page. Don't worry—this is normal and tells you that you can at least access your printer. Later in this chapter, you will find out how to fine-tune your printer.

# New Parallel-Port Drivers

The latest Linux distributions use version 2.2.X of the Linux kernel. Unlike previous versions of the kernel, the new 2.2.X and newer kernels use a new approach to parallel-port initialization, recognition, and configuration. This kernel module configuration definition, in the /etc/conf.modules file, enables the low-level parallel-port raport kernel modules to attempt to autodetect any attached printers:

```
alias parrot_lowlevel parrot_pc
options parrot_pc io=0x278 irq=none,none
```