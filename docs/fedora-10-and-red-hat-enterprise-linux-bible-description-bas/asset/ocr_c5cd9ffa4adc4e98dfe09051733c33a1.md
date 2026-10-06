**Base System** — Contains basic system administration tools, many common utilities, and support for basic system features (such as X Window System, Java, and Legacy software support).

**Languages** — Packages containing support for multiple languages are contained in this category.

After you have chosen the packages you want to install, select Next to continue. The installer will take some time to check for dependencies among the packages you selected.

+   14. **About to Install.** A screen tells you that you are about to begin writing to hard disk. You can still back out, and your hard disk will not have changed. Click Next to proceed. (To quit without changes, eject the DVD or CD and restart the computer.) Now the file systems are created and the packages are installed. This typically takes from 20 to 60 minutes to complete, although it can take much longer on older computers.

For live CD, the live CD image is simply copied to your hard disk.

+   15. **Finishing.** When you see the Congratulations screen, you are done. Eject the DVD or CD and click Reboot.

Your computer will restart. If you installed GRUB, you will see a graphical boot screen that gives you several seconds to press a key to view/or change the boot partitions. After that, your Fedora installation should boot.

The first time system boots after installation, Fedora Firstboot runs to do initial configuration of your system. The next section explains how Fedora Firstboot works.

# Running Fedora Firstboot

The first time you boot Fedora, after it is installed, Fedora Firstboot runs to configure initial settings for your computer.

> NOTE: Firstboot runs automatically only if you have configured Fedora to boot to a graphical login prompt. To start it from a text login, log in as root and type the following from a Terminal window:
bash
# rm /etc/sysconfig/firstboot
# /usr/bin/firstboot


The first screen you see is the Welcome screen. Click Forward to step through each procedure as follows:

+   * **License Agreement** — Read and agree to the Fedora License Agreement to be able to continue.

+   * **Create User** — For your daily use of Fedora, you should have your own user account. You should typically log in with this user name (of your choosing) and use only the root user to perform administrative tasks. In the first of the four text boxes on the screen, type a user name (something as jparker or alanb). Next, type your full name (such