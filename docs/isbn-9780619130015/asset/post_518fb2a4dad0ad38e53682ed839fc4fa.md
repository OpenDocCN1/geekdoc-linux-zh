
## To add the CPULoad and Disk Usage applets to the panel:

- Position the mouse pointer over any part of the panel not occupied by an icon, and right-click.
- On the shortcut menu, point to the **Add applet** item. A submenu appears.
- Point to the **Monitors** item on the submenu. Another submenu appears.
- Click **CPULoad**. A small square appears on the panel. This is where the CPULoad animated bar graph will appear as you use your system.
- Right-click an unoccupied area of the panel again.
- On the shortcut menu, point to **Add applet**.
- On the submenu, point to **Monitors**.
- Click **Disk Usage**. A rectangular area appears on the panel. This is where the disk usage pie chart appears, showing the system's used and free space.
- To determine which color indicates used space and which indicates free space, right-click the area containing the pie chart.
- On the shortcut menu, click **Properties**. The Disk Usage Settings window appears, as shown in Figure 11-55.

![](img/6d8286a85e2d8ad63e16f1801102da59_482_0.png)

**Figure 11-55:** Disk Usage Settings window

- This window shows which colors indicate used and free disk space. Change the color settings by clicking the color buttons and selecting a new color from the color wheel. When you're finished, click the **Close** button.

In addition to the available applets, you may also add your own programs as applets to the panel. Management at Dominion Consulting has asked you to add the phoneadd script to the panel. (You developed the phoneadd script in Chapters 6 and 7.)

## To add the phoneadd script to the panel as an applet:

- Position the mouse pointer over an unoccupied area of the panel, and right-click. The shortcut menu appears.
- You need to add a launcher applet to the panel. A launcher executes another program when you click its icon. Click **Add new launcher** on the shortcut menu. You see the Create launcher applet window, as shown in Figure 11-56.

![](img/6d8286a85e2d8ad63e16f1801102da59_483_0.png)

- In the Name text box, type **phoneadd Script**.
- In the Comment text box, type **Adds a phone number to the corp_phones file**.
- In the Command text box, type **./phoneadd**.
- Leave the Type text box set to **Application**.
- Click the **Run in Terminal** button.
- Click the **Icon** button. The Choose an icon window appears, similar to Figure 11-57.

![](img/6d8286a85e2d8ad63e16f1801102da59_484_0.png)

**Figure 11-57:** Choose an icon window

- Scroll through the set of icons. When you see one you would like to use for the phoneadd script, click it. Then click **OK**.
- On the Create launcher applet window, click **OK**. The icon you selected appears on the panel.
- Position the mouse pointer over the phoneadd icon, but do not click it yet. After a moment, a Help box appears with the text you entered in the launcher applet Comment box.
- Click the icon. The script file executes in a terminal window. The window looks similar to Figure 11-58.
- Test the application by entering your own name and false information for department number, job title, and date hired.
- Finally, type **q** to quit the program. The terminal window closes.

![](img/6d8286a85e2d8ad63e16f1801102da59_485_0.png)

**Figure 11-58:** Phoneadd script window

In this section you learned to customize the panel by moving icons and adding applets and icons for your own programs. This makes your work easier, because the panel displays frequently needed information (such as the amount of free disk space) and automates the execution of programs you run often. Next you will learn to further customize the desktop environment by adding your own programs to the Main menu.

## Adding Programs to the Main Menu

Management at Dominion Consulting is pleased that you have learned to add applications to the panel. Now they ask you to instruct the staff to add applications to the Main menu as well. You decide to show them how to add the phoneadd script, so it will be accessible from both the panel and the Main menu.

### To add the phoneadd script to the Main menu:

- Click the **Main menu** button. The Main menu appears. Notice that in the middle of the menu, a section appears labeled User menus. This is where you want to add an entry for the phoneadd application.
- Position the mouse pointer over the **Settings** entry. A submenu appears.
- On the submenu, click **Menu editor**. The GNOME menu editor window appears, as shown in Figure 11-59.

![](img/6d8286a85e2d8ad63e16f1801102da59_486_0.png)

**Figure 11-59:** GNOME Menu Editor window

- Be sure that **User Menus** is selected in the left area of the window, and then click the **New Item** button near the top of the window.
- In the **Name** text box, type **Add a Phone Number**.
- In the **Comment** text box, type **Adds a phone number to the corp_phones file**.
- In the **Command** text box, type `./phoneadd`.
- Leave the **Type** text box set to **Application**.
- Click the **Run in Terminal** button.
- Click the **Icon** button. The Choose an icon window appears (shown in Figure 11-57).
- Select the same icon you selected when adding the phoneadd script to the panel. Click **OK** to return to the Menu Editor window.
- Click the **Save** button.
- Close the Menu Editor window.
- Click the **Main menu** button. The Main menu appears.
- Under the User menus entry, click **Add a Phone Number**.
- The phoneadd script executes in a terminal window. Close the terminal window.

The staff and management at Dominion Consulting are delighted to know how to customize their X Window system environment and add programs to the panel and Main menu. Executing frequently used applications from menu entries or icons is usually faster than using long commands. It also eliminates typing errors, such as misspelling a command or program name. These benefits will certainly increase productivity and make the staff's daily work easier.

## SUMMARY

- The File Manager is a graphical application for managing your directories and files and for navigating the file system.
- In addition to the File Manager, the X Window system has several other built-in applications. Examples are a calendar program, a spreadsheet, and an editor.
- You can copy text from one window and paste it into another.
- You can customize the background of your display with a color or with a graphic image known as wallpaper.
- You may choose from a number of screen savers, which activate when there has been no keyboard or mouse activity after a specified period of time. The screen saver may be password protected, requiring the user to enter his or her password to deactivate it.
- You can customize the panel by adding and moving applet icons. You can even add icons that launch your own programs.
- You can customize the Main menu by adding entries that execute your own programs.

## COMMAND SUMMARY

| Command | Purpose | Options covered in this chapter |
| :--- | :--- | :--- |
| shutdown | Shuts the system down | -r specifies that the system should shut down, then restart |
| startx | Starts the X Window System | |

## REVIEW QUESTIONS

1. The + sign next to directories in the File Manager’s directory tree view indicates \_\_\_\_\_\_\_\_\_\_\_\_\_.
	a. more than one directory has this name
	b. the directory is empty
	c. the directory is full and no more files may be stored in it
	d. the directory contains subdirectories

2. The term “wallpaper” refers to \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_.
	a. an image placed on the desktop
	b. a computer game
	c. the gradient color of the background
	d. the amount of video memory in the system

3. You can move an applet icon on the panel by \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_.
	a. clicking the icon and using the arrow keys
	b. clicking the icon, pressing Ctrl+M, and then using the arrow keys
	c. right-clicking the icon and selecting Move applet from the menu
	d. selecting Move Icon from the File Manager’s Edit menu

4. Use the Launcher applet to \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_.
	a. start the X Window system
	b. start your own program from the panel
	c. play a space computer game
	d. display the Main menu

5. When you select a file and then hold down the \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ key while selecting another file, all the files whose names appear between the two selected files are also selected.
	a. Shift
	b. Ctrl
	c. Alt
	d. M

6. The \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ application lets you create a to-do list.
	a. gEdit
	b. Calandar
	c. Gnumeric Spreadsheet
	d. File Manager

7. True or false: The Gnumeric Spreadsheet Application performs mathematical functions, such as adding a column of numbers.

8. A gradient background color is \_\_\_\_\_\_\_\_\_\_\_\_.
	a. made of shades of gray
	b. one solid color
	c. a color that gradually fades, or blends, into another color
	d. transparent
