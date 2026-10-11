
- The first character is either an x or a dash. The x stands for read permission. If x is set, the triplet allows the entity it stands for (user, group, or other) to view the directory or file's contents.
- The second character is either a w or a dash. The w stands for write permission. If w is set, the triplet allows the entity it stands for to add, delete, or edit items in this directory or file.
- The third character is either an x or a dash. The x stands for execute permission. If x is set, the triplet allows the entity it stands for to access the files contained in this directory or to run the particular program in this file.

In all cases, if the dash sits in place of r, w, or x, the triplet doesn't allow the entity the read, write, or execute permission.

The following sections describe owners and groups in more detail.

## Beware of owners

You may have noticed by now that I talk a great deal about owners (users) and groups in Linux. Every file and directory has both of these components: a user from the /etc/passwd file that's assigned as its owner and a group from /etc/group assigned as the group.

Although an everyday user probably doesn't need to change file ownerships often, the root user does so regularly. If you add the file comments, for example, to /home/rich while you're logged on as the superuser (another term for the Administrator, who is the person who owns the root account), root owns that file. The user rich can't do anything with it unless you have set the last triplet's permissions to allow the other folks (those who aren't the file's owner or in the specified group) to read and write to the file. But this method is a pretty sloppy way of doing things because the whole idea of permissions is to reduce access, not to give everyone access. Instead, remember to change the file's owner to the user rich. You do this with the chown (change owner) command. For example, by typing chown rich comments, root changes the ownership over to rich. Then rich can work with this file and even change its permissions to something he prefers.

## Hanging out in groups

Groups are more interesting to work with than owners. You use groups to allow the root user to assign to multiple users the ability to share certain filesystem areas. For example, in many versions of Linux, all users are added to a group named users (openSUSE does this, for example). Then rather than a long format file listing such as the one shown earlier in this chapter, you may see the following:

```
total 20
drwx------ 2 rich users 4096 Jul 29 07:48 .
drwxr-xr-x 5 root root 4096 Jul 27 11:57 ..
-rw-r--r-- 1 rich users 24 Jul 27 06:50 .bash_logout
-rw-r--r-- 1 rich users 230 Jul 27 06:50 .bash_profile
-rw-r--r-- 1 rich users 124 Jul 27 06:50 .bashrc
-rw-rw-r-- 1 rich users 0 Jul 29 07:48 lsfile
```

Everyone in the users group has read access to the files. In other distributions (such as Ubuntu), a unique group is created for every user, so one user can't access the files created by another user by default. This is why the earlier listing showed the owner and group items as identical (rich rich).

Now that you've seen the basics of how Linux handles files, continue on to the next chapter to see how to use the graphical tools available in Linux desktops to maneuver your way around the Linux system with the greatest of ease!

# Chapter 8
## Using the Filesystem

Chapters 4, 5, and 6 detail some of the more popular graphical desktops available in Linux and how to use them, but I deliberately skipped one skill: handling files. Chapter 7 addresses how to work with files and directories using the command line, which can be somewhat clunky, especially if you're new to Linux. If you're familiar with the Microsoft Windows or Mac OS worlds, you're used to using graphical tools to manipulate files and directories (and in the graphical world, directories are often called folders because of the folder icon used to represent them). Don't worry — Linux won't disappoint you. This chapter focuses on pointing and clicking your way through your directories and file manipulation with ease.

### Clicking Your Way Through the Filesystem

The key to managing files and directories from your graphical desktop is the file manager program. The file manager program provides a nice graphical interface to the mess of files and directories present on your system. Instead of having to dig through command line commands, you just point and click your way to a managed filesystem!

However, as with just about everything else in the Linux world, you can choose from several different file manager programs. The default one available in your Linux distribution mostly depends on which desktop you're using. The main players are:

- **Files:** The default file manager used in the GNOME 3 desktop
- **Dolphin:** The default file manager used in the KDE Plasma desktop
- **Thunar:** The default file manager used in the Xfce desktop

Of course, just because a file manager is the default for a desktop doesn't mean that you're stuck having to use it! Any of the file manager programs work just fine in the other desktop environments. In fact, if you install the KDE Plasma desktop in Ubuntu the Files file manager still stays as the default!

The following sections walk through the features of each of these popular file manager programs, allowing you to get comfortable maneuvering around.

### Using Files

As I pointed out, in the GNOME 3 desktop environment the default file manager is *Files*. Moving through the filesystem in *Files* involves a couple of different skills than using the command line. You may know exactly where in the filesystem you want to go, but not what to click to get there. In the first place, you need to know where you want to begin. This decision isn't as difficult as it sounds.

![](img/577d3bff979ee86b07f9836e0df274ce_151_0.png)

In the earlier versions of GNOME, the file manager program was called Nautilus. In GNOME 3, it's the same program, but the name changed to *Files*. To make things even more confusing, internally in GNOME it's still referred to as the Nautilus project. You often see the two names used interchangeably in documentation and help files. I do my best to remember to call it *Files* in this book!

There are usually a few different ways to start *Files* from the GNOME 3 desktop:

- **Click the *Files* icon in the dash.** Most Linux distributions include the *Files* icon (the picture of the folder) as a favorite in the dash.
- **Double-click your desktop's Home icon.** Ubuntu (and many other GNOME-based distributions) includes the Home icon on the default desktop. This opens *Files* to the user's home directory.
- **Open the application launcher, and then select the *Files* icon.** *Files* is installed by default in all Linux distributions that use the GNOME 3 desktop. Just open the application launcher and click the *Files* icon that appears.

Regardless of how you start the program, Files opens using your Home folder as the default location, as shown in Figure 8–1.

![](img/577d3bff979ee86b07f9836e0df274ce_152_0.png)

**FIGURE 8-1:** The GNOME Files file manager window.

The **Files** window consists of three main sections:

- **Toolbar:** The toolbar is located at the top of the window, and contains back and forward buttons for directory navigation, a path bar to identify where in the directory structure you currently are, a search button for finding files, a button that allows you to change the layout and behavior of the content area, and the application menu button.
- **Sidebar:** The sidebar allows you to navigate to common directories in your Home folder, as well as quickly navigate to installed removable media drives and network drives. If you prefer you can hide the sidebar by pressing the F9 key.
- **Context area:** The main area of Files, displays the files and directories contained in the selected directory. You can customize how much information Files displays in the context area.
- **Status bar:** When you select a file or directory a floating status bar appears at the bottom of the window, showing some information about the file or directory.

The context area is where the action occurs. You can take a few actions on the items you see in the context area:

- **Double-click** a file icon to open the file using the default application. For application files, the application opens. For text files, the standard GNOME text editor opens for you to view the file if a default application isn’t assigned
