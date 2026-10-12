
# Figure 3-3: The Installing Packages window.

4. Click the Reboot button when prompted, and remove the companion Fedora Core 3 DVD (or CD-ROM) from the computer.

   Your computer reboots and the Display settings window opens. If you want, you can reconfigure your display settings and video card; you can also configure them for a dual head (two side-by-side) display.

5. Click OK.

6. Click Next in the warning dialog box that opens.

Fedora Core is installed! The following section helps to finish various post-installation tasks that will make your Fedora Core computer easier to use.

## Post-Installation: Using the Setup Agent

After your computer reboots and the Display settings window closes, the Setup Agent opens. The Setup Agent simplifies the installation process by pushing some configuration work to the post-installation phase. Your new Fedora Core computer will work just fine whether or not you run the Setup Agent — but a little fine tuning makes it work better.

The Setup Agent automatically runs the first time you boot your computer after installing Fedora Core. The Agent asks you to read and accept the Fedora Core license, reconfigure your monitor (optional), create a user login account, (recommended; use the root account for system administration), set the date and time, test your sound card, and install any optional software packages.

The process of configuring these individual systems is described throughout this book. However, the following steps describe how to use the Setup Agent immediately after completing the Fedora Core installation:

1. When your new Fedora Core computer boots (starts), you see the Setup Agent’s Welcome screen. Click the Next button to start the post-installation configuration process.

   The License Agreement window opens.

2. Gather your lawyers (guns and money are optional) and read the agreement together. Click the button labeled Yes, I agree to the License Agreement and then click Next and proceed to court.

   Truthfully, going to court is unlikely. But, just in case, deny everything.

3. The Date and Time window appears. You can change the date and time if you need to.

   You can also let your computer automatically and continuously update your clock. If you plan to be connected to the Internet, either through a LAN (local area network) or a broadband modem (DSL or cable), click the Network Time Protocol tab and select the Enable Network Time Protocol (NTP) option. Select an NTP server from the drop-down menu of NTP servers and click the Add button. The default choices clock.redhat.com and clock2.redhat.com work well, but you can enter one you want. Alternatively, you may have access to an NTP server not on the list and can enter it manually. Click the Forward button to continue to the Sound Configuration screen.

   We recommend that you use the NTP option if your computer is connected continuously to the Internet on an Internet-connected LAN, a DSL connection, or a cable modem. PC clocks tend to drift from seconds to minutes per day. It's better to be up to date than not.

4. Click the Next button.

5. The Display window opens. Change your monitor type, display resolution and the colors depth, if you want.

   You can change the monitor type by clicking the configure bar and selecting from the drop-down menu that opens. Change the resolution and/or color depth by clicking on the appropriate bar and selecting a value.

6. Click the Next button.

   The System User window opens. Only the root user account was created during the installation process. You have the chance here to create one or more user accounts.

7. Enter an account name, the name of the account owner, and its password. Click the Next button to continue.

   If you’re connected to a LAN that provides a network login (such as a Kerberos network), click the Use Network Login button and select the appropriate option. You most likely encounter a network login only when you’re connected to a large corporate network. It’s beyond the scope of this book to describe this particular plethora of situations. Consult your system administrator.

8. Fedora Core does a good job of detecting hardware, such as sound cards, and should detect yours. Click the Play test sound button to test your audio system.

   A dialog box opens, asking whether you heard the music.

9. Click Yes if you hear the penguin playing the guitar.

   An Error dialog box opens if you click No.

10. Click OK to continue.

    If the sound test fails, consult the section in Chapter 12 for help with setting up your sound system. Click the Forward button to continue.

11. Click the Next button.

    The Additional CDs window opens. The companion Fedora Core DVD doesn’t include any additional software, so you have nothing to do here.

12. Click the Next button.

    The Finish Setup window opens.

13. Click the Next button. The Setup Agent closes and your Fedora Core computer is ready to use.

![](img/41feae212f5c6612ff709354891f7b39_62_0.png)

You can run Setup Agent whenever you want. The Setup Agent is a script named *firstboot*. You can run the Setup Agent by running the *firstboot* script with the *reconfig* option. Just log in as *root* and run the following commands from a GNOME Terminal window:

```bash
rm /etc/sysconfig/firstboot
/usr/sbin/firstboot
```

That’s it! You have built yourself a Fedora Core computer. After your computer reboots itself, you can then use it as your personal workstation.

# Part I: Installing Fedora Core

# Chapter 4

# Getting to Know Fedora Core

- In This Chapter
  - Booting your Fedora Core computer
  - Logging in to your Fedora Core computer
  - Using graphical and text-based applications and utilities
  - Setting up your monitor and video card
  - Getting to know the Fedora Core file system
  - Making user accounts for the first time
  - Logging out of your Fedora Core computer

If you have installed Fedora Core, you should spend a few minutes studying some basics before you start using it. This chapter covers just enough, but no more, of the Linux fundamentals needed to get you started. We cover topics such as starting and stopping your Fedora Core computer, understanding the difference between graphical and nongraphical applications, and how Linux uses files.

We start by describing how to start your new Fedora Core computer. This process is simple, but it’s helpful to know more about it.

## Booting Your Fedora Core Computer

To boot a computer means simply to start it or turn the power on; to reboot a computer means to restart it. The following steps describe how to boot your Fedora Core computer:

1. Make sure that your computer is turned off.
2. Turn on the power to your computer.

After a short time, the Fedora Core boot menu appears on your screen. If you have only Fedora Core installed on your computer, you're given only one choice of operating systems to boot: Linux (see Installation Stage 2: Slicing and Dicing the Pie in chapter 3 for more information about dual-booting).

![](img/41feae212f5c6612ff709354891f7b39_65_0.png)

3. Press the **up-** and **down-arrow** keys to highlight the word *Linux* (if it's not highlighted already) and then press **Enter**.

   - If you don't press any of the keys, the default operating system (that is, Fedora Core, which sets itself as the default when you install it) starts automatically after a 10-second delay.
   - If you're running more than one operating system (for example, Fedora Core and Windows), you can select any of the listed operating systems to boot; we assume here that you choose Linux.

After you press **Enter**, Fedora Core boots. During this process, a graphical progress window shows how far along the boot process is. You can (optionally) display lots of technical information by clicking the Show details button. The optional information is what Linux is learning about your computer and its hardware (disk drives, networks, and memory, for example).

## Logging In to Your Fedora Core Computer

When you use Fedora Core (or any Linux distribution), you must log in as a particular user with a distinct login name. Why? Because Linux is a multiuser system — therefore it uses different accounts to keep people from looking at other people's secret files, erasing necessary files from the system, and otherwise (intentionally or unintentionally) doing bad things.
