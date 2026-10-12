As the Linux kernel starts, you see a long list of opening messages often referred to as the *boot messages* (you can see these messages at any time by typing the `dmesg` command in a terminal window). These messages include the names of the devices that Linux detects. One of the first lines in the boot messages reads

> Calibrating delay loop... 2957.31 BogoMIPS

*BogoMIPS* is Linux jargon (explained in this chapter in a handy sidebar) for a measure of time. The number that precedes *BogoMIPS* depends on your PC's processor speed, whether it's an old 200MHz Pentium or a new 4GHz Pentium 4. The kernel uses the BogoMIPS measurement when it has to wait a small amount of time for some event to occur (like getting a response back from a disk controller when it's ready).

After the boot messages, Fedora Core switches to a graphical boot screen that shows information about the progress of system startup. Specifically, you see information such as servers being started and hardware being probed.

When you boot Fedora Core for the first time after installation, you get the Firstboot program that displays a welcome screen and asks you to agree to the Fedora Core license agreement (it's the GNU General Public License). Click the Yes radio button and then click Next. After that Firstboot takes you through date and time setup (see Figure 4-1), display setup, user account setup, sound card check, and, finally, gives you a chance to install programs from any additional CDs.

![](bbox=[0.25, 0.64, 0.72, 0.9])

# **Figure 4-1:** Configure date and time from this screen in Firstboot.