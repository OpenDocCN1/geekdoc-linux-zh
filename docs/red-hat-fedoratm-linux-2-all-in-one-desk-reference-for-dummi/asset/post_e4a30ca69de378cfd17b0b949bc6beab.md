
![](img/9f89727199836b0f871f1745838aa8b2_116_0.png)

You will find that KDE is very easy to use and is similar in many ways to the Windows GUI. You can start applications from a menu that’s similar to the Start menu in Windows. As in Windows, you can place folders and applications directly on the KDE desktop.

### **KDE panel**

The KDE panel appearing along the bottom edge of the screen is meant for starting applications. The most important component of the panel is the **Main Menu** button on the left-hand side of the panel. That button is like the Start button in Windows. When you click the **Main Menu** button, a pop-up menu appears. From this menu, you can get to other menus by moving the mouse pointer over items that display a rightward-pointing arrow. For example, Figure 4-17 shows a typical menu selection for configuring various services.

You can start applications from this menu. That’s why the KDE documentation calls the **Main Menu** button (of course, the KDE documentation refers to the button as the **K** button) the *Application Starter*.

![](img/9f89727199836b0f871f1745838aa8b2_117_0.png)

Next to the Main Menu button, the panel includes many more buttons. If you don't know what a button does, simply move the mouse pointer over the button; a small pop-up window displays a brief message about that button.

Table 4-1 gives you an idea of what happens when you click each of the major buttons on the KDE panel. When you have some time, try these buttons one by one to get a feel for what you can do in KDE.

**Table 4-1 KDE Panel Buttons**

| When You Click | It Does This |
| :--- | :--- |
| ![Image of a hand clicking a button] | Shows the application menu from which you can start any application. |
| ![Image of a web browser icon] | Starts the Mozilla Web browser. |
| ![Image of an envelope icon] | Starts the Ximian Evolution e-mail and calendaring software. |
| | Runs OpenOffice.org Writer, a Microsoft Word-like word processor. |
| | Runs the OpenOffice.org Impress slide presentation program that’s similar to Microsoft PowerPoint. |
| | Runs OpenOffice.org Calc, a Microsoft Excel-like spreadsheet program. |
| | Runs Print Manager, a utility that enables you to set up and monitor print queues. |
| | Switches to the desktop whose number you have clicked. |
| | Runs Klipper, the KDE clipboard utility for cutting and pasting information. |
| **20:42** | Displays the current time. Click to view the current month’s calendar. Right click for the menu to adjust the date and time. |

### **Customizing the KDE desktop**

KDE makes customizing the look and feel of the KDE desktop easy. Everything you have to decorate the desktop is in one place: the KDE Control Center. To start the KDE Control Center, choose Main Menu->Preferences->More Preferences->Control Center.

When the KDE Control Center starts, it displays the main window with a tree menu on the left side and some summary information about your system in the workspace to the right, as shown in Figure 4-18.

The KDE Control Center’s tree menu shows the items that you can customize with this program. The tree menu is organized into categories such as Appearance & Themes, Internet & Network, Peripherals, Security & Privacy, and so on. Click the plus sign (+) to the left of an item to view the subcategories for that item. To change an item, go through the tree menu to locate the item and then click it. That item’s configuration options then appear in a tabbed dialog box on the right side of the window.

![](img/9f89727199836b0f871f1745838aa8b2_119_0.png)

**Figure 4-18:** The initial window of the KDE Control Center.

### *Changing the background*

To change the desktop's background, choose Appearance & Themes→ Background. A tab appears (as in Figure 4-19) that shows the options for customizing the desktop's background.

If you want to change the background of a specific desktop, click the Setting for Desktop drop-down menu. From the list of desktops, you can select the desktop whose background you want to change.

For a colored background, select the No Picture radio button. From the Colors drop-down menu, you can select either a single color background or a variety of color gradients (meaning the color changes gradually from one color to another) or a picture (an image used as a background). You can then pick the two colors by clicking your color buttons that appear under the Colors drop-down menu. After making your selections, click Apply to try out the background. (If you don't like what you get, click Reset to revert to the previous background.)

If you want to use a picture as background, select the Picture radio button and then click the folder icon next to that radio button. A dialog box comes up, showing the JPEG images in the `/usr/share/backgrounds/images` directory. You can select any one of these images and click OK. Then click the Apply button in the KDE Control Center to apply this wallpaper to the desktop. If you don't like the appearance, click Reset.

![](img/9f89727199836b0f871f1745838aa8b2_120_0.png)

## **Logging out of KDE**

When you're done exploring KDE, log out. To log out of KDE, choose Main Menu→Logout. You can also right-click empty areas of the desktop and choose Logout from the pop-up menu that appears.

## **Playing with the Shell**

Fedora Core is basically UNIX, and UNIX just doesn't feel like UNIX unless you can type cryptic commands in a text terminal. Although GNOME and KDE have done a lot to bring us into the world of *windows*, *icons*, *mouse*, and *pointer* (affectionately known as *WIMP*), sometimes you're stuck with nothing but a plain text screen with a prompt that looks like this (when you log in as *root*):

```
[root@localhost etc]# 
```

You see the text screen most often when something is *wrong* with the X Window System, which is essentially the machinery that runs the windows and menus you normally see. In those cases, you have to work with the shell and learn some of the cryptic Linux commands.

You can prepare for unexpected encounters with the shell by trying out some Linux commands in a terminal window while you're in the GNOME or KDE GUI. After you get the hang of it, you might even keep a terminal window open, just so you can use one of those cryptic commands simply because it's faster than trying to point and click (those two-letter commands do pack some punch).

### **Starting the Bash shell**

Simply put, the shell is the Linux *command interpreter* — a program that reads what you type, interprets that text as a command, and does what the command is supposed to do.

Before you start playing with the shell, open a terminal window. In either GNOME or KDE, select Menu → System Tools → Terminal. What appears is a window with a prompt, like the one shown in Figure 4-20. That’s a terminal window, and it works just like an old-fashioned terminal. A shell program is running and ready to accept any text that you type. You type text, press Enter, and something happens (depending on what you typed).

![](img/9f89727199836b0f871f1745838aa8b2_121_0.png)

The prompt that you see depends on the shell that runs in that terminal window. The default Linux shell is called *Bash*.

Bash understands a whole host of standard Linux commands with which you can look at files, go from one directory to another, see what programs are running (and who else is logged in), and a whole lot more.

In addition to the Linux commands, Bash can run any program stored in an executable file. Bash can also execute *shell scripts*, text files that contain Linux commands.

### **Understanding shell commands**

Because a shell interprets what you type, knowing how the shell figures out the text that you enter is important. All shell commands have this general format:

```
command option1 option2 ... optionN
```
