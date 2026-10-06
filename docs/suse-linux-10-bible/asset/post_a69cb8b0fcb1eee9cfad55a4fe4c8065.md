
# Chapter 9 ♦ Configuring the System with YaST 247

When the user list has loaded, you can either edit (select the user and press Edit) or create a new user. We will go ahead and create a new user, Roger Whittaker.

To create a new user:

- 1. Click Add. You will be presented with a dialog box very similar to what you see when you use SUSE, with YaST asking you about the user (see Figure 9-24).

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_291_0.png)

Figure 9-24: Creating a new user

- 2. To create the user, click Create. If you want to set specific settings for the user, you can select either Password Settings or Details.

- a. You can change quite a few things about how the user's password is used in the system. Click Password Settings.

In Figure 9-25, you can see that you can set the amount of days before the user is warned of a password expiry (where they need to change their password), the amount of times the user can log in to their account after their password expires (use -1 to allow them to always log in to their account once the password has expired), and the amount of days the same password can be valid, along with the minimum. You can also set the amount of time the account itself is active.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_292_0.png)

Figure 9-25: Editing password settings

For example, if you had an account on site for the next two weeks, you could set the expiry date to be two weeks in the future (in the format of YYYY-MM-DD).

To save the password settings, click Next.

- b. To select specific information for the user roger, click the Details button. You will be presented with the User ID, home address, the comment field (a free-form field allowing you to enter any information about the user, such as their description and so forth), the default login session, and the user's default group, along with any other groups the user should be part of.

One of the most important parts of this section is the Additional Group Membership. If you have created other groups or are going to separate your users into specific groups, you can add the user to the group here. By default, normal users are associated with audio (to access the sound card), dialout (to access the modem), lp (to access the terminal), and video (to access advanced features of the video card).

- 3. When you are happy with the settings for the user account, click Next. You are returned to the user information screen, where you can click Create to save the user to the system.

- 4. To return to YaST, click Finish.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_293_0.png)

Figure 9-26: Changing account settings

## Adding or Editing Groups

To create or edit groups in your system, select Security and Users -> groups. From the User section, you are presented with a list of groups currently on the system (see Figure 9-27). You can select a group from the list and click Edit to change settings for group, or click Add to create a new group.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_293_1.png)

Figure 9-27: List of groups installed in your system

If you click Add to create a new group, you are presented with the screen in Figure 9-28. Here you can enter the group name, the group ID (it is safe to use the default), and also the option to use a password for the group.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_294_0.png)

Figure 9-28: Adding a new group to the system

Users are able to change their default group for a session by using the newgrp command. For example, if a user wants to change his default group from users (the default) to dev, he can use the command newgrp dev. If a password is set for this group, he must enter it before he can change to this group.

If you want to add any users to this group, you can select them from the right-hand pane. When you are happy with the group, click Next. Now you are returned to the group list where you will see your new group. Click Finish to return to YaST.

## Installing Additional Software

Unless you install every available package when you install your SUSE system, you'll eventually need (or read about) some additional software from SUSE distribution CDs or DVD. Chapter 12 explains how to install additional software packages from the command line, but if this is on SUSE CDs or DVD, you'll have to figure out where to find it first. Luckily, SUSE's YaST tool makes it easy to locate and install additional software from your SUSE media.

YaST's Install and Remove Software module can be started from within YaST by selecting Software icon in YaST's left pane and selecting Software Management from the left pane or Install and Remove Software icon in YaST's right pane. You can also start this module by typing:

```
yast sw
```

If you start the module from within KDE Control Center, YaST prompts you for the root password before allowing you to continue.

When the module starts (see Figure 9-29), it displays a dialog that makes it easy to search for packages by name, view the summary that describes the package, its size, and so on.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_295_0.png)

Figure 9-29: YaST's Software Management Module

As an example, suppose you've read about emacs in this book and want to see if emacs-related packages are available on your SUSE distribution. To do this, enter emacs in the Search box and click Search. The Install and Remove Software window displays all packages with emacs in their Name or Summary. A check mark displays next to the name of all packages that are already installed, as shown in Figure 9-30.

To install a package that is not installed, click the checkbox next to its name in the package listing and then click Accept to proceed with the installation process. For example, to install the qemacs (Quick Emacs) package, a small lightweight version of emacs, click the checkbox next to its name and then click Accept. YaST analyzes all dependencies required by the selected package, adds those to the list of packages to install, and proceeds to install the selected packages. If the media from which you installed SUSE is not in your CD or DVD drive, YaST prompts you for the appropriate disk, as shown in Figure 9-31.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_296_0.png)

Figure 9-30: Installed packages matching emacs

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_296_1.png)

Figure 9-31: Install for necessary media

After the selected package(s) have been installed, YaST runs SuSEconfig to ensure that any libraries installed with the package are available to the system and prompts you as to whether you want to search for and install additional packages, or click Finish to close the Install and Remove Software dialog box.

## YOU – The YaST Online Update

Software is one of things that is never finished. In the open source world, we tend to be more honest about this than ever before; Linux and all the software running on it is in a constant state of change and improvement. At the same time, there are security issues. Again, the open source mentality for openness about the fact that these security issues exist provides rapid fixes.

For several years, SUSE has provided an online method of updating the system; this operates collecting patch RPMs from a server and installing them through the YaST online update module. The beauty of patch RPMs is that they need to contain only the changed files from an RPM that has been updated, significantly reducing the bandwidth involved in the update procedure.

## YOU on SUSE Professional and on SLES

The online update on SUSE Linux Enterprise Server (SLES) and the other SUSE products are the means by which the paid-for software maintenance system is applied to your server. As such, it requires authentication: your 14-digit key password to be put into the YaST Online Update (YOU) module for it to authenticate against the server in Germany. SLES 9 offers a YaST module to assist with setting up a local YOU server.

In the case of Professional, although the online updater comes with no guarantees, it is a free part of the system, there is a choice of installation servers offering the RPMs, and no registration is required to use it.

## susewatcher

SUSE Linux Professional includes a system applet called susewatcher. This displays an icon that indicates whether an update is required. It does this by checking the state of the system against a remote server. If automatically checks for updates in the susewatcher main screen (see Figure 9-32), then susewatcher will generally check whether updates to the currently set of software are available. If updates are available, it changes the appearance of its icon in the system tray:

- A red icon with an exclamation mark indicates that security updates are required.

- A smiling geeko icon indicates that all available updates have been made.

- If there is a green icon with a white page symbol overlaid on it, all available updates have been applied, but you have not yet read the update messages by clicking the susewatcher Show Messages button.
