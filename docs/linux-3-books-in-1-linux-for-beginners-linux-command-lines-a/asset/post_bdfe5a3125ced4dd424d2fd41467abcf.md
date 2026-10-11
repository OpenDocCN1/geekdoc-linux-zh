
The system you are installing Ubuntu on may have additional hardware such as a graphic card and a Wi-Fi network card. The open-source drivers included in the Ubuntu installation may not support your hardware by default. This is when this option should be enabled so that the installation downloads third-party drivers for your hardware if required.

![](img/aae83b54a1b1783f3f5369bd9062b27c_43_0.png)

## Disk Partitioning

The next screen gives you a window to choose the type of installation. The first option lets you do an Ubuntu installation from scratch. Note that this will erase everything on your hard disk and install Ubuntu. If this is what you wish to do, you can stop reading here and go to the next step.

If you already have sufficient knowledge about operating system installations, you may also want to look at the Advanced Features. You can use this option if you want to create custom disk partitions and for some additional options such as:

- *Use LVM with the New Ubuntu Installation*

LVM or Logical Volume Management is a tool that can be used to create virtual drives on Linux. It is very similar to the `gparted` tool.

## Encrypt the New Ubuntu Installation for Security

You can enable this option if you wish to encrypt all the data on your hard drive, including the installation files. You will get an option to create a decryption key that can be used later to decrypt the data.

If you wish to create custom partitions, you can select *Something Else*.

When you select this option, you will be taken to a screen to create custom partitions. You can create physical partitions, and Linux will consider these partitions as individual physical hard drives.

You can apply the changes you made to the disk partitions by clicking on Continue.

You will receive a confirmation box that says *Write changes to disks?* This is your last chance to review the partition changes, and only after you click Continue on this screen, your partitions come into effect.

## Selecting the Time Zone

When the installation concludes, you need to set up your timezone.

Type your city's name in the box. This will help the system set the time zone for your system. Click on Continue.

You will be able to change the timezone later as well from the Ubuntu desktop.

## Create User Account

On the next screen, you will be prompted to create a user account. You will need to enter the following details to create a user account.

- **Name:** Type in your name here
- **Computer Name:** You can provide a hostname for your system here
- **Username:** This will be the account name for your user
- **Password:** Enter a password of your choice and ensure that it is strong. The installer will let you know the strength of your password.
- **Log in Automatically:** This option should not be enabled ideally.
- **Require my password to log in:** Ideally, this option should be enabled.

Click on Continue to process with the installation.

The installer will start writing Ubuntu files to your hard disk, and this can take some time depending upon your system's hardware. After the installation is complete, unplug the bootable USB drive from your system. You will be prompted to restart the system. Click on Restart Now.

![](img/aae83b54a1b1783f3f5369bd9062b27c_45_0.png)

The system will restart and should now boot into the newly installed Ubuntu 20.04 LTS.

You have now successfully installed Ubuntu on your system. If your system is connected to a network via Ethernet or Wi-Fi, you will see prompts to download and install updates. It is advisable to install the updates and keep your system up to date.

In this chapter, we went through the most common Ubuntu installation wherein a bootable USB drive is created, and Ubuntu is installed from scratch on your system, which may have had Windows before. There are other methods to install it, too, wherein you can install Ubuntu and still keep your Windows operating system as well. This is done by creating the Ubuntu installation on a different partition than the Windows operating system installation. We do not cover that kind of installation in this book, as this is a book for beginners.

# Chapter Four

## Getting Started with Ubuntu

Now that you have installed Ubuntu, it is time to start using your Linux operating system. Unlike the paid operating systems such as Windows or macOS that require you to pay more to get additional software, Ubuntu already comes loaded with the software you need to get started. You will find everything in Ubuntu right from an office suite, a web browser, to email media tools. You are good to start with using Ubuntu as soon as the installation is completed.

Everyone uses a computer in their unique way, and every user likes to customize the look and feel of their computer to their requirements. Keeping this in mind, Linux lets you use one of the many graphical interfaces that it has to offer. Thus, there are hundreds of graphical interfaces available on Linux to suit every user's needs.

Although there are multiple graphical interfaces available for Linux, two of them are the most popular ones, GNOME and KDE. Each of these environments has a user-friendly and easy-to-use interface. They have a few differences concerning the look of the desktop and how they can be personalized further.

The KDE environment gives a user complete control and configuration options to personalize the desktop. The user can configure every aspect of the desktop and has the liberty to modify the desktop's look and feel.

GNOME, on the other hand, is inspired by the desktops of Windows and macOS and prioritizes simplicity. GNOME can be customized easily, too but hides certain options from the user.

Ubuntu users can choose either of these two desktop environments along with some more desktop environments as well.

The default desktop environment in Ubuntu 20.04 is GNOME 3.36, but this does not mean that you cannot install other desktop environments. Let us see what it has to offer to its users.

### Theme

Ubuntu 20.04 LTS comes with a revamped Yaru theme, and you can see it right from boot up to the desktop. Developers of operating systems like to have a distinctive look for their operating system, which helps establish their brand's image. In January 2020, Canonical, the parent company of Ubuntu, had a design sprint in collaboration with the Yaru team and the Ubuntu design team. Yaru was introduced in Ubuntu 18.10.

Yaru has three types of variations, and it also has a sound theme. During the design sprint, the designers and developers also identified some UI improvements that could benefit the desktop. You can switch your desktop theme between Light, Standard, and Dark colors using the Appearance settings. You can also use the default sound alert that Yaru provides.

![](img/aae83b54a1b1783f3f5369bd9062b27c_48_0.png)

The revamped Yaru theme also lets you make changes to the boot splash screen and the installer windows. The Yaru team has now implemented the spinner that was available only on the desktop to appear even on the boot screen. If you have installed the system using the full-disk encryption option, then the boxes for the passphrase in the boot menu will match the desktop theme too.

Ubuntu has received a new animal mascot with each major release lately. This time also, a neatly designed creature has been integrated for the release. They have also given it a name. The Ubuntu 20.04 LTS mascot is called Felicity.

![](img/aae83b54a1b1783f3f5369bd9062b27c_49_0.png)

The default theme wallpaper features Felicity. The theme also has some more wallpaper in addition to the mascot wallpapers. All the images come from a copyright-free website, and every image is very focal.

## GNOME 3.36

Ubuntu has defaulted to the GNOME desktop as the default desktop environment ever since the release of Ubuntu 17.10. The Ubuntu team has worked deeply with the GNOME developers and the Ubuntu community to create a solid GNOME experience for Ubuntu users. Ubuntu also has ties with the developers at Debian to keep updating GNOME to the latest packages.

GNOME 3.36 has changes that are visible to the user for a beautiful user
