
## Chapter Five

### Things to Do After Installing Ubuntu 20.04 LTS

The codename for Ubuntu 20.04 LTS is Focal Fossa. Ubuntu has always been proud about shipping the operating system with inbuilt applications that can help a user get started soon after installation. The default apps and settings are set as per what most people like. But we do not want to assume that you are most people. You may not want everything, or you may want more than the default offerings.

This chapter will help you tweak Ubuntu 20.04 LTS to improve your Ubuntu experience.

### What’s New?

Every version of Ubuntu differs from its previous release, and Ubuntu 20.04 LTS is no exception. The boot time on the Ubuntu 20.04 has been improved considerably, thanks to the new kernel compression algorithms. We have already discussed the Yaru theme and the OEM manufacturer’s logo showing up on the boot splash as well.

### The Dark Mode

The dark mode is the latest for any device today, be it a mobile or a computer. Everyone wants to have a dark mode on their devices, which is now possible with Ubuntu.

The dark mode does not default in Ubuntu, but you can easily switch to it. Follow the steps given below.

- Open Settings > Appearance
- Select ‘Dark Windows’ setting

That is it. You will see that the change is immediate, and everything is darkened immediately, from backgrounds to toolbars. Even all the applications will not have a dark theme to them.

It is worth noting that the dark mode will not have any effect on the user interface of the GNOME shell in Ubuntu, such as calendar, notifications, and system menus.

If you get tired of the dark mode, you can always switch to the default theme again from the Appearance settings panel.

### Tweaking GNOME

GNOME tweaks is an application through which you can customize your desktop even more.

You will get options to:

- Move window buttons from the default right to left
- Change some themes
- Change the font and font size of your desktop
- Display weekdays on the clock
- Switch between workspaces
- Centre new windows automatically
- And more

Ubuntu tweak is an application through which you can fine-tune your desktop.

Launch Firefox on your Ubuntu system and go to the link `apt://gnome-tweaks` to install GNOME tweaks.

### Get a Powerful Tool for File Previews

There is a tool known as GNOME Sushi that is a spacebar preview tool available for the GNOME shell desktop.

If you have been a Mac user, you will know what a spacebar preview means. Apple’s operating system was the first one to have this feature, and it became trendy. You can select a file in the file manager and hit your spacebar to have a quick preview of that file.

Similarly, you can use Sushi to preview media, images, documents, get information about a file or a folder, and so on, without having to open a dedicated application to do it. Also, when you finally find the file that you want to open, Sushi gives you an option to do that.

Sushi is free and open-source, just like Ubuntu. You will be able to find it on the Ubuntu software app by searching for it by its name. Or you can simply launch Firefox again and type in the URL `apt://gnome-sushi`

### Minimizing Applications

In Windows, when you click on any application on the taskbar, it gets minimized. This feature is not enabled by default on Ubuntu, but you can enable it.

This setting is not easily available via the user interface, but you can do it via the command line.

Simply open the Linux terminal and type the following command to enable minimize for Ubuntu.

```
gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'
```

This will be effective immediately. You can now click on any app on the dock, and you will see that it gets minimized.

### Display Battery Percentage

This feature is useful if you have installed Ubuntu on a laptop and you want to see your battery percentage at a glance. It lets you know how much battery percentage is remaining without opening the status bar to do so.

You will need to use the GNOME tweaks app for this that we discussed above.

1. Launch GNOME Tweaks
2. Select Top Bar
3. Enable the Battery Percentage setting

You can also enable this via the command line by typing the following command on the terminal.

```
gsettings set org.gnome.desktop.interface show-battery-percentage true
```

### Tweaking Touchpad Scroll

If you have installed Ubuntu on a laptop and are not comfortable with the default scroll of the touchpad known as ‘Natural Scrolling,’ you have the option to change it. You can change it such that the content moves in the direction of your scroll, that is, scroll down to move the page downwards.

1. Open Settings
2. Select Mouse & Touchpad
3. Toggle the Natural Scrolling option to On

That is it, and you should now be able to scroll comfortably as per your liking.

### Setting up Livepatch

Livepatch is an option in Ubuntu that lets you have the Linux kernel updated automatically without the need to reboot your system.

This feature is aimed at servers, but it works just fine on desktops as well.

Launch the Livepatch application from the Application grid, and you’re all set to install security updates to your Linux kernel without needing a reboot after installation.

### Automatic Trash Deletion

There is an automatic trash deletion option hidden in the Privacy options in Settings. You can simply enable it so that trash is deleted at regular intervals. It is very useful to automatically free up space if you forget to do it manually from time to time.

### Installing Amazing Software

You can find both free and paid software for Ubuntu. But which software would you need?

You can go through the Ubuntu software app and install software that you believe will suit your needs.

### Don’t Do On Your Ubuntu System

There are a few things that are not advisable to do on your Ubuntu 20.04 LTS system. Let's go through them in brief.

- Do not uninstall the default desktop

The default desktop environment in Ubuntu is the GNOME shell desktop. Not every user will like the desktop, but Ubuntu gives you the option to install other desktop environments alongside the default GNOME Shell, but uninstalling the default desktop environment after installing a new one is a poor decision. It can hamper system performance and result in irreversible damages if you uninstall your Ubuntu system's default desktop environment.

- Do not run random commands

You will find millions of scripts for Linux all over the Internet claiming to do something amazing. While some of them are genuine, a majority of them can damage your system.

The thumb rule to follow is if you do not know the function of a particular Linux command, do not run it. This should be followed even strictly for commands that will perform multiple functions in one go. Always review the content of a script before you fire it on your terminal.

## Chapter Six

### The Linux Command Line

In this chapter, we will take you through the Linux command line. The Linux command line is similar to the command prompt in Windows and can be used to perform almost every task that you can do through a graphical interface by using the command line instead. By the end of this chapter, you would be proficient in managing your files and directories through the command line.

### The Bash Shell

BASH, short for Bourne-Again Shell, is a Linux utility that helps you interact with the operating system through the command line. It is the first choice of shell on every Linux distribution, and naturally, you will find it on Ubuntu as well. The Bash shell can be accessed on Ubuntu through a utility called the terminal.

You can launch the terminal on Ubuntu by selecting the Application button on the lower-left corner of your desktop and then click on All at the bottom of the screen. Continue to select Utilities, and you will see all the system tools under Utilities. Click on Terminal to launch it.

Upon launching the bash shell, you will see a string that indicates that input is expected from the user. This string is called shell prompt. If you are the root user or the superuser for your Ubuntu system, the prompt will end with a # sign. If you are a non-root user, the prompt will end with a $ sign.

```
[root@desktop ~]#
[student@desktop ~]$
```

As mentioned, the Linux Bash shell is just like the command prompt available in Windows, but both use a different scripting language, and the scripting language in the Bash shell is much superior as compared to the one available in the Windows PowerShell utility. You can automate numerous
