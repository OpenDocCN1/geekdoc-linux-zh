![](bbox=[0.24, 0.09, 0.75, 0.21])

Figure 6-3: Code maturity level options

If you aren't sure what a particular option for the kernel is used for, click help. This is a really great feature if you aren't really sure if you want to compile something into your kernel or not. You should get a detailed message such as the one shown in Figure 6-3.

+   2. Loadable module support – Turn this on to use modules (loadable portions of the kernel). You don't necessarily need to use modules; however, as the kernel development heads more in the direction of modules instead of built-in support, you may want to experiment with this option. If you have already activated loadable module support, you may also want to specify the autoloading of modules – after all, such convenience does seem to be why they exist – although you can certainly load them by hand if you wish. Because I use the Zip drive and it's not always attached, I compiled loadable module support with autoload in my kernel. The loadable module is shown in Figure 6-4.

![](bbox=[0.24, 0.58, 0.72, 0.72])

Figure 6-4: Loadable module options

+   3. General setup – General setup is the basic hardware setup for the system you installed Slackware on. Unless you're working on a 486 or earlier hardware, you don't want to enable math emulation. Turn on PCI Bios, networking support, and kernel support (at least for the ELF binaries). You'll also want to compile your kernel as ELF. I included both a.out and ELF binary support for my kernel, enabled networking and IPC support. The other options include the processor type, memory options, and other general things you may or may not want running on your system. I left alone. The General Setup is shown in Figure 6-5.