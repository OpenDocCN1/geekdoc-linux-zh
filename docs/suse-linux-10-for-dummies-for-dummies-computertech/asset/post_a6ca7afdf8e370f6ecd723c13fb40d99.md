
If you want to change the background of a specific desktop, click the Setting for Desktop drop-down list. From the list of desktops, you can select the desktop whose background you want to change.

For a colored background, select the No Picture radio button. From the Colors drop-down list, you can select either a single color background or a variety of color gradients (meaning the color changes gradually from one color to another) or a picture (an image used as a background). You can then pick the two colors by clicking the color buttons that appear under the Colors drop-down list. After making your selections, click Apply to try out the background. (If you don't like what you get, click Reset to revert back to the previous background.)

The default KDE desktop uses a picture as the background. If you want to use a different picture as background, select the Picture radio button and then click the folder icon next to that radio button. A dialog box comes up, showing the JPEG images in the /usr/share/wallpaper directory. You can select any one of these images or pick an image from another directory and click OK. Then click the Apply button in the KDE Control Center to apply this wallpaper to the desktop. If you don't like the appearance, click Reset.

## Getting to Know GNOME

GNOME (pronounced *Guh-NOME*) is another GUI for SUSE Linux. The acronym GNOME stands for *GNU Network Object Model Environment* (and GNU, as you probably know, stands for *GNU's not UNIX*). GNOME is a graphical user interface (GUI) and a programming environment. From the user's perspective, GNOME is like Microsoft Windows. Behind the scenes, GNOME has many features that allow programmers to write graphical applications that can work together well. In this chapter, I point out only some key features of the GNOME GUI, leaving the details for you to explore on your own at your leisure.

If you're curious, you can always find out the latest information about GNOME by visiting the GNOME home page at www.gnome.org.

If you installed GNOME as your desktop, you see the GNOME GUI desktop (refer to Figure 5-2) after you log in. The GNOME desktop is very similar to the Windows desktop albeit with two taskbars — one at the top and the other at the bottom of the screen, and icons for folders and applications appear directly on the desktop.

### The GNOME panels

The GNOME panels are key features of the GNOME desktop. In the default configuration, the desktop has one panel at the top and the other along the bottom of the screen. You can simply drag and move the panels to any edge of the screen, but it's best to leave them alone. When you drag the panel to a side, the panel's size changes, and the icons can get enlarged. That makes it hard to access the menus.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_91_0.png)

Think of the top GNOME panel as your gateway to the things you can do. From the menus and buttons on that panel you can start applications. Think of the bottom panel as information about the things you have done so far. For example, the bottom panel shows buttons corresponding to applications that you have started so far.

Figure 5-8, earlier in this chapter, shows a typical top panel that shows menus, application launcher buttons, and small panel applets. Each panel applet is a small program designed to work inside the panel. For example, the Clock applet on the panel's far right displays the current date and time.

The GNOME desktop's top panel (refer to Figure 5-8) has three menu buttons — Applications, Places, and Desktop — at the left edge:

- **Applications Menu** has the menu of applications, organized by category. I refer to the Applications Menu as the Main Menu because this is the primary menu for starting applications.
- **Places Menu** has options for opening your home folder, viewing the desktop, browsing the computer, connecting to various servers such as FTP and Windows shares, and searching for files.
- **Desktop Menu** has the menu for system configuration and performing tasks such as getting online help and logging out or locking the screen.

The buttons to the right of the menu buttons are launcher applets. Each of these applets displays a button with the icon of an application. Clicking a button starts (launches) that application. Try clicking each of these buttons to see what happens. Move the mouse over a button and a small Help message appears with information about that button. That's how you can easily tell what each button does.

### Customizing the GNOME desktop

By now, you may be itching to do a bit of decorating. After all, it's your desktop. You can set it up any way you want it to. To change the GNOME desktop's background, right-click on an empty area of the desktop and select Change Desktop Background from the menu that appears. The Desktop Background Preferences dialog box appears, as shown in Figure 5-13.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_92_0.png)

From this dialog box, you can select a background of a solid color, a color gradient, or a *wallpaper* (an image used as the background). A *color gradient* background starts with one color and gradually changes to another color. The gradient can be in the vertical direction (top to bottom) or horizontal (left to right).

Just for the fun of it, if you want to try out a horizontal color gradient, follow these steps:

1. Scroll up the Desktop Wallpaper list (refer to Figure 5-13) and select No Wallpaper from the very top of the list.
2. Click the Desktop Colors item, and from the drop-down list, choose the Horizontal Gradient option.
3. Click the Left Color button next to the drop-down list.

   The Pick a Color dialog box comes up (shown in Figure 5-14) from which you can select a color.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_93_0.png)

Figure 5-14: The Pick a Color dialog

4. Repeat the same process to select the right color.

After you complete these steps, the desktop shows the new background color.

To revert back to the original wallpaper, scroll down in the Desktop Wallpaper list (refer to Figure 5-13) and select the previous wallpaper image (or pick a different wallpaper, if that's what you want).

Click Close to get rid of the Desktop Background Preferences dialog box.

## Chapter 6: Finding and Organizing Files

### In This Chapter

- Understanding how Linux organizes files
- Navigating the file system with Linux commands
- Understanding file permissions
- Manipulating files and directories with Linux commands

To use files and directories well, you need to understand the concept of a hierarchical file system. Even if you use the GUI file managers to access files and folders (folders are also called _directories_), you can benefit from a file system that gives you the lay of the land.

In this chapter, I introduce you to the Linux file system, and you discover how to work with files and directories with several Linux commands.

### Figuring Out the Linux File System

As with any other operating system, Linux organizes information in files and directories. Directories, in turn, hold the files. A _directory_ is a special file that can contain other files and directories. Because a directory can contain other directories, this method of organizing files gives rise to a hierarchical structure. This hierarchical organization of files is called the _file system_.

The Linux file system gives you a unified view of all storage in your PC. The file system has a single root directory, indicated by a forward slash (/). Within the root directory is a hierarchy of files and directories. Parts of the file system can reside in different physical media, such as a hard drive, floppy disk, and CD-ROM. Figure 6-1 illustrates the concept of the Linux file system (which is the same in any Linux system whether it's SUSE, Red Hat, or what have you) and how it spans multiple physical devices.
