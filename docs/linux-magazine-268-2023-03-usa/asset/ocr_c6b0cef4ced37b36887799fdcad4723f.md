# # IN-DEPTH
## Bash Tray Scripts

# ## Customize your
### system tray with YAD

## BESPOKE
### SYSTEM TRAY

![](bbox=[0.35, 0.0, 0.95, 0.32])

YAD lets you customize your system tray with one-line Bash tray scripts. By Pete Metcalfe

My goal was to find a simple way to group together my favorite apps and web pages into a system tray item.

There are a number of different approaches to this, but for my requirements I found that the YAD (Yet Another Dialog) tool [1] gave me everything that I needed, and I could do it all with just one line of Bash script.

In this article, I will introduce Bash tray scripts with three examples. The first example will show how to create tray scripts that put Linux diagnostic data into both custom dialogs and terminal windows. In the second example, I will add pop-up browser windows to a right-click submenu. The final example will look at how to toggle the tray icon, command, and tooltip with simulated weather conditions.

```
Listing 1: Creating a System Tray Item
```
yad --notification --image="gtk-execute" \\
--command="yad --text="$ (lsusb)\\" \\
--title="USB Info"" --fixed --button=ok \\
--text="My Fav Utility"
```
```

# ### Getting Started

There are a number of different tools for creating system tray applications, such as AllTray and KDocker. For my projects, I prefer YAD because it lets you create custom dialogs and it supports dynamic changes to the tray features. YAD is a command-line dialog tool very similar to Zenity [2], but with some added features such as system tray support and a more complete dialog functionality.

For Debian/Raspian/Ubuntu systems, you can install YAD with:

```
```bash
sudo apt install yad
```
```

# ### Creating a Tray Script

Listing 1 is a one-line Bash script that calls YAD to create a system tray item (Figure 1). Because Bash and YAD statements can be quite long, you can make the code more readable by using backslash (\) characters to extend a statement across multiple lines, as shown in Listing 1.

The yad statement in Listing 1 uses the --notification and --image options to put a user-defined icon in the system tray. The --command option calls an application or script when you click on the tray item. The -textl option defines tooltips.

In Figure 1, the command-line lsusb utility lists the USB-connected devices. The output from lsusb is shown in a YAD text dialog.

To terminate a YAD tray script, use a center mouse click. You can also terminate from a right-click menu, which I'll discuss later.

![](bbox=[0.62, 0.76, 0.94, 0.9])

Figure 1: A one-line Bash script creates a system tray item that displays the output from !susb in a dialog.
*Photo by Soliyeon Cho on Unsplash*