# **490 Part III: Troubleshooting**

Unless you have a (really old) processor without a math coprocessor built in, choose the default by pressing Enter here.

**MTRR (Memory Type Range Register)** support (**CONFIG_MTRR**) [Y/n/?/]

*This is probably the first question that does not quite make sense to you (unless you are an expert in x86 CPU design) and to most beginning kernel hackers. So what should you choose here? While the default option is often the right one in most cases, in this case you can find what Memory Type Range Register (MTRR) support means by entering ? at the prompt. You get the help screen as shown here:*


```
CONFIG_MTRR:
```

```
On Intel Pentium Pro and Pentium II systems the Memory Type Range
Registers (MTRRs) may be used to control processor access to memory
ranges. This is most useful when you have a video (VGA) card on a
PCI or AGP bus. Enabling write-combining allows bus write transfers
to be combined into a larger transfer beforeburst over the
PCI/AGP bus. This can increase performance of image file operations
2,5 times or more. This option creates a /proc/mtrr file which may
be used to manipulate your MTRRs. Typically the X server should use
this. This should have a reasonably generic interface so that
similar control registers on other processors can be easily
supported.

Saying Y here also fixes a problem with buggy SMP BIOSes which only
set the MTRRs for the boot CPU and not the secondary CPUs. This can
lead to all sorts of problems.

See Documentation/mtrr.txt for more information.

You can safely say Y even if your machine doesn't have MTRRs; you'll
just add about 3K to your kernel.

As you can see, this is quite helpful. Because I am configuring this kernel
for a server, I do not care much about the video, so I chose "N" here.

```

Symmetric multi-processing support (**CONFIG_SMP**) [Y/n/?]