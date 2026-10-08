
## Chapter 2: Installing Ubuntu

FIGURE 2-3
Specifying a language when booting the Desktop CD

| Amharic | Norsk bokmål | 中文(简体) |
| --- | --- | --- |
| Arabic | Gujarati | Norsk nynorsk | 中文(繁体) |
| Estonian | Hindi | Pashto (Guremukhi) |
| Bulgarian | Polab. | Português do Brasil |
| Bengali | Hrvatski | Português |
| Maori | Bahasa Indonesia | Русский |
| Catalan | Italiano | Šamgilli |
| Czech | 日本語 | Slovenčina |
| Danish | azo | Slovenščina |
| Deutsch | Khmer | Svenska |
| Estonian | Shqip | Tamil |
| Finnish | kurdi | |
| Esperanto | Lietviešu | Thai |
| Español | Latvieki | Tagalog |
| Euskara | Macedonian | Türkçe |
| Somali | Malayalam | Ukrainська |
| Français | Nepali | Tiếng Việt |
| Gaelic | Nederlands | |

To continue, use the cursor keys to select your language and press Return. If you do not select a language within 30 seconds, English will be used as the default language. The traditional boot menu for the CD displays, as shown in Figure 2-4.

FIGURE 2-4
Boot options from the Ubuntu Desktop CD

![](img/1a233c34336fbf5a85d6eb785e401709_74_0.png)

## Part I: Getting Started with Ubuntu

This screen is similar to the boot screens for the Ubuntu Server/Alternate CDs (discussed in Chapter 3) and older versions of the Ubuntu Desktop CD. This screen enables you to select whether you want to boot from the Desktop CD to try Ubuntu, install Ubuntu, test the CD for defects, test your system's memory, or ignore the Desktop CD and boot from the system's first hard drive.

To boot Ubuntu Linux on your system so that you can experiment with it without making any changes to your system (generally referred to as test-driving), press Return or wait 30 seconds, at which point your system will automatically boot from the Desktop CD. If you're booting from an Ubuntu Desktop CD, the standard Ubuntu Desktop displays, as shown in Figure 2-5.

FIGURE 2-5

The standard Ubuntu desktop from the Desktop CD

![](img/1a233c34336fbf5a85d6eb785e401709_75_0.png)

Once you're running Ubuntu from the Desktop CD, you can:

- Install the distribution from the Desktop CD as described in the next section.
- Test-drive Ubuntu using the menus that are available in the upper-left corner of the screen and sample the files provided in the Examples folder.

Experimenting with Linux after booting from a Desktop CD is described in the section, "Test-Driving Ubuntu Linux," later in this chapter. When test-driving Ubuntu, you can practice running specific applications and even experiment with installing and configuring the software that is discussed in the remainder of this book.

## Installing Ubuntu from a Desktop CD

There are several ways to use a Desktop CD to install Ubuntu on a computer system:

- Boot from the CD, wait until the screen shown in Figure 2-2 displays, and click "Install Ubuntu 10.04."
- Boot from the CD, press a key while the boot screen shown in Figure 2-1 displays, set your language, use the arrow keys to select the "Install Ubuntu" option, and press Return or Enter on your keyboard.
- Boot from the CD, press a key while the boot screen shown in Figure 2-1 displays, set your language, and press Return or Enter on your keyboard to boot the "Try Ubuntu without any change to your computer" option. If your system boots, double-click the Install Ubuntu 10.04 icon on the desktop.

These two methods run the same to permanently install Ubuntu on your computer system. The instructions in this section describe how to install, or end-user, version of Ubuntu from an Ubuntu Desktop CD that is included with this book. See Chapter 3, "Installing Ubuntu on Special-Purpose Systems," for information about installing other versions of Ubuntu Linux, such as the Ubuntu Server or OEM distributions, which require you to have a different installation CD from the Ubuntu web site. For an overview of the different Ubuntu CDs, see section of Chapter 1, "The Linux Project," entitled "Ubuntu CDs."

### Caution

If you are installing Ubuntu onto a system on which another operating system is already installed, make sure you have backed up any data that you want to preserve removable media such as a CDROM, DVD, USB flash drive, and so. If you continue using that operating system, the Ubuntu installer does a great job of automatically re-partitioning your disk so that you can boot your computer either your existing operating system or Ubuntu, but nothing is perfect, and "soft" is a big part of "software." It is completely impossible to have two backups of your critical data. If your computer already has another operating system installed on all hard drive(s) that you want to preserve, the Ubuntu installer will automatically offer to resize the existing operating system partitions and install Ubuntu as an alternate operating system on your machine.

You'll need to supply a few pieces of information during the installation process so that Ubuntu is correctly configured for your system, language, and geographic location. The installation process is as follows:

1. The dialog shown in Figure 2-6 prompts you to specify the location and associated time zone where you will be using your computer. This value is used to further customize the language that you selected in the previous screen by the appropriate date and time formats, numerical conventions, and currency values for your geographic location. If the time zone that is initially displayed is incorrect, click the map in your approximate location, or select a time zone or city from the Zone pop-up menu. Once you have selected an appropriate time zone or city, click Forward or press Return to proceed to the next screen.

## FIGURE 2-6

Specifying your geographic location

![](img/1a233c34336fbf5a85d6eb785e401709_77_0.png)

## FIGURE 2-7

Specifying your keyboard type

2. The dialog shown in Figure 2-7 prompts you to specify the type of keyboard attached to your computer. The default value is based on your settings on previous screens — if this is incorrect, click “Choose your own” and select your keyboard type from the full list of supported keyboard types. You can enter sample text into the text area at the bottom of the screen to verify that the correct symbols are displayed as you type. Once you are sure the correct keyboard is set, click Forward to proceed.

![](img/1a233c34336fbf5a85d6eb785e401709_77_1.png)

3. The dialog shown in Figure 2-8 enables you to select where you want to install Ubuntu. This dialog looks different and provides different options depending on how disks in your system are currently configured and what partitions they already contain (if any). Figure 2-8 shows the screen that you would see if you were installing Ubuntu on a system where no operating system is currently installed.

## FIGURE 2-8
Specifying where you want to install Ubuntu

![](img/1a233c34336fbf5a85d6eb785e401709_78_0.png)

The option that you want to select on this screen therefore depends on the current state of your system's hard drive(s), how many hard drives are present in the system, and where you want to install Ubuntu. Your options are as follows:

- If you are installing on a new computer or hard drive, the "Erase and use the entire disk" option will be selected, as shown in Figure 2-8.
- If you are installing Ubuntu on an x86 or 64-bit PC system on which an operating system is already installed and do not have unallocated space on your disk, the "Install them side by side, choosing between each startup" option will be selected, as shown in Figure 2-9.
- If your system already contains an operating system but you do not want to preserve it, you can select the "Erase and use the entire disk" option to erase your existing operating system and install Ubuntu on the entire disk. The image of your disk at the bottom of the screen will be updated to illustrate that you will be using the entire disk, as shown in Figure 2-10.
- If your system contains multiple hard drives, they will all be listed in this dialog. Select the disk upon which you want to install Ubuntu.
