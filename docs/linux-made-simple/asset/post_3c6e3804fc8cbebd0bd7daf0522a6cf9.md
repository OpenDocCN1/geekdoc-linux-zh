
pressure from end users and provided a UEFI update on its website to enable the required options – Advent’s DT2410 PC is an example where this happened.

With your Windows system backed up and the UEFI configured correctly, it’s time to press on and install Ubuntu alongside your existing setup. One of the reasons we’ve chosen Ubuntu is that its user-friendliness is apparent from the moment you install it. The set-up process is painless and relatively straightforward to follow: pop your cover disc into the drive, start your PC and, if necessary, select your optical drive from the boot menu. When the cover disc menu appears, choose the Ubuntu option to begin.

Wait for a few minutes, then after a short pause, when the screen goes grey and then red, the Welcome screen will appear. You’ll be given the option of either trying Ubuntu or installing it – select the ‘Install’ option. Next, tick both boxes: ‘Download updates while installing’ and ‘Install this third-party software’. Click ‘Continue’, then wait while the updates are downloaded in the background.

## Install Ubuntu 14.04 LTS

The Installation Type screen should then appear. In most cases, it should seamlessly detect your Windows installation – leave ‘Install Ubuntu alongside…’ and click ‘Continue’.

If Windows isn’t offered as an option, this means Ubuntu hasn’t detected it. If you’re running a newer PC with a UEFI installed in place of the traditional BIOS, you’ll need to make sure you boot from the optical disc using the same option that Windows was installed with. Reboot your PC, then choose the alternative optical disc option from the boot menu to see whether Ubuntu now detects your Windows installation. If the option doesn’t appear whether you choose UEFI or the legacy option, it could be down to your partition table containing both MBR and GPT records (see below for the step-by-step guide for a way to resolve this issue).

The next screen sees Ubuntu automatically find some free space for itself – either by carving up your current Windows partition, or by locating more space on another attached drive and repartitioning that instead. If you don’t want it installing on a USB drive, power down your PC, disconnect the offending drive, then start again. Ubuntu needs a

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_34_0.png)

Check your UEFI shell’s boot settings to see whether Legacy, UEFI or mixed mode is selected.

minimum of 6.4GB of free space, but will take up to 40-odd GB if it can. You can alter this figure by clicking and dragging the grey space between both suggested partitions. It’s smart enough to not allow you to swallow up your entire Windows partition, but if you plan to continue using it going forward, try to leave at least 10GB of free space if you can, and preferably more. In most cases, the default choice should be fine anyway, so click ‘Install Now’. Note the comment about partition resizing, and click ‘Continue’.

Next you’ll be prompted to choose your region – the installer should automatically detect this – then click ‘Continue’ to select your keyboard layout. In most cases, the default UK keyboard layout is the one to pick, so click ‘Continue’ again. You’ll now be prompted to enter your name. As you enter it, Ubuntu will populate both the computer’s name and username fields based on your choice – you’re free to edit both should you choose. The final choice available to you is to pick a password. Select one that you’ll easily remember, because you’ll need this not just to log into Ubuntu but also to perform administrator-level tasks. Click ‘Continue’ again, and you can sit back and wait for Ubuntu to install itself on your PC – it really is that simple. It’s worth hanging around because the installer will reveal some useful pointers for your first steps into using Ubuntu. But turn the page and we’ll take you on your own personal tour of your shiny, new desktop and operating system.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_34_1.png)

## Fix Windows detection issues

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_34_2.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_34_3.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_34_4.png)

### 1 Launch Ubuntu Live

If your Windows install isn’t detected, click ‘Back’ until you return to the Welcome screen. Click ‘Try Ubuntu’ to load the live CD. When it’s loaded, press [Ctrl]+[Alt]+[T] to open a terminal window. Type the following command and hit [Enter]:

```
sudo gdisk /dev/sda
```

### 2 Verify and fix

If gdisk says it’s found both an MBR and a GPT, then the presence of GPT is the problem – removing it will enable Ubuntu to see your Windows partition. First, select the GPT entry by typing 2 and hitting [Enter]. When prompted, type x and hit [Enter] to access Expert command mode.

### 3 Apply and reboot

Type z and hit [Enter]. When prompted to wipe the GPT on /dev/sda, type y and hit [Enter]. When asked if you’d like to blank the MBR, make sure you type n, hit [Enter] and close the terminal, then reboot and try to install Ubuntu again. This time you’ll see the option to install it alongside Windows.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_35_0.png)

## Get started with Ubuntu

Take your first steps into the Unity desktop.

You've installed Ubuntu, removed the cover disc and rebooted your PC. The first change you'll see is the presence of a new boot menu on startup, called GNU Grub (see 'All about Grub', p19). This enables you to choose which OS to boot into, plus gives you access to a memory testing utility. The default choice is Ubuntu, but before booting into it for the first time, we recommend selecting the Windows entry. This lets Windows boot for the first time since the Ubuntu installer resized your partitions – you'll note it immediately runs the disk checking tool to verify and update its own partition records. Let it do this, then once complete, it'll restart your PC. Select 'Windows' again from the Grub boot menu to check all is well. Assuming it is, restart your PC again.

This time, leave 'Ubuntu' selected and hit [Enter] to boot into your new OS for the first time. After the loading screen flashes by, you'll be prompted to enter the password you set up during installation. Type this in, hit [Enter] and you'll arrive at Ubuntu's desktop, which is called Unity.

The Unity desktop shares a number of similarities with Windows, such as the presence of shortcut icons on the left, but you'll also notice some key differences, which will feel more familiar to those who have used a Mac before. First, the Menu Bar at the top of the screen works in a similar way to the Windows Taskbar Notification area, with a number of icons providing access to key tools. From the off you'll see – from left to right – network, keyboard, volume, date/time and settings. Most of these are self-explanatory – simply click one to reveal its Options menu.

The 'Settings' button is the most interesting of these – not only does it provide access to the power options, but it also enables the ability to quickly switch users, log out or lock the computer, and it also provides a handy shortcut to Ubuntu's System Settings, more on which in a moment.

When you open an app, its title will also appear in the Menu Bar – roll your mouse over the Menu Bar and its menu items will appear, and clicking one will open its menu.

## The App Launcher

The shortcut icons displayed on the left-hand side of the screen are part of Unity's App Launcher. Rather than cluttering up your desktop with lots of icons, these are all housed in a single column – simply roll your mouse to the bottom or top of the launcher to reveal more shortcuts. The App Launcher houses shortcuts to applications, workspaces, removable drives and the rubbish bin. The two shortcuts at the top, however, are of particular interest: the top one enables you to quickly search your computer and the internet from one handy window, while the Files shortcut gives you access to a file manager, making it easy to browse, access and manage your files – again, more on that later.

To find out more about a shortcut, roll your mouse over it and its title will pop up. Click one to open it. As time moves on, you'll want to know how to add and remove shortcuts from the App Launcher – to remove a shortcut, simply right-click it and choose 'Unlock from Launcher'. The simplest way to add a shortcut is to use the search tool to locate the app in question, then simply click and drag its shortcut into place on the Launcher. You can also reorder items in the Launcher by simply clicking and dragging them to their new spot.

The desktop itself works in a similar way to that of Windows, and can be used to house files, folders and shortcuts should you wish to clutter it up – again, it uses the familiar right-click menu to provide you with options for

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_35_1.png)

The main distinction for former Windows' users trying out the Unity desktop environment for the first time will be the position of the launch bar.

## Get more apps

Ubuntu 14.04 LTS ships with a few apps pre-installed – notably LibreOffice and the Firefox web browser. For a complete list of installed apps, open the Ubuntu Software Center and select the 'Installed' button. Expand a category to see what apps are there, such as Rhythmbox. Use the Search box to locate them, then either open them directly from here or drag a shortcut on to the App Launcher. There are many more apps you can add to your Ubuntu installation, and the vast majority are free. There's a number of ways to do this: as you've seen with Ubuntu Tweak (see 'Accessing your documents', above-right), you can download apps from the web or install them from our cover disc. If they're packaged as Deb files, you can double-click them and have the Ubuntu Software Center manage installation. You can also search for more apps from within the Software Center, too – just use the search box. The Ubuntu Software Center isn't a definitive source for apps, however – Linux apps are housed in special collections called repositories, and as you'll see over the page, you can install apps via the terminal, too. One thing you'll want to do is access apps for specific file types, such as images. If you can't find an app, try double-clicking a file you want to open – if you get a 'Could not display' error, click 'Yes' to search the Ubuntu repos for apps.
