![](bbox=[0.05, 0.12, 0.92, 0.62])

# Figure 6-18: Creating a Boot Diskette

A boot diskette can be handy for a number of reasons:

+   - **Use It Instead of LILO** — You can use a boot diskette instead of LILO. This is handy if you're trying Red Hat Linux for the first time, and you'd feel more comfortable if the boot process for your other operating system is left unchanged. With a boot diskette, going back to your other operating system is as easy as removing the boot diskette and rebooting.
+   - **Use It In Emergencies** — The boot diskette can also be used in conjunction with a rescue disk, which will give you the tools necessary to get an ailing system back on its feet again.
+   - **Use It When Another Operating System Overwrites LILO** — Other operating systems may not be as flexible as Red Hat Linux when it comes to supported boot methods. Quite often, installing or updating another operating system can cause the master boot record (originally containing LILO) to be overwritten, making it impossible to boot your Red Hat Linux installation. The boot diskette can then be used to boot Red Hat Linux so you can reinstall LILO.