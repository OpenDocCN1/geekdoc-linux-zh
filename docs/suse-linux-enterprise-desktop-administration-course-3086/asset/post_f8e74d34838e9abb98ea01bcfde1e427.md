
![](img/9129877170834ca9d5fdac5319bf5f12_106_0.png)

## section 4
## Administer Linux with YaST
**YaST is a powerful tool to configure your SUSE Linux Enterprise Desktop 10.** Many modules are available to perform important configuration tasks. This section covers the hardware information module, change date and time module, language settings module, and keyboard module. Other modules will be covered in other sections of the course.

## Objectives
- Objective 1—YaST Basics
- Objective 2—Become Familiar with YaST Modules
- Objective 3—Understand the Role of SuSEConfig

## Objective 1—YaST Basics
YaST stands for *Yet another Setup Tool*. You can use YaST to complete many configuration tasks as a SUSE Linux Enterprise Desktop administrator.

The YaST user interface can appear in two kinds:
- *ncurses*—Text mode
- *Qt*—Fully graphical mode

The appearance of the user interface depends on which command you use to start YaST and on whether you use the graphical system or the command line, as indicated in Table 4.1.

| Command | Terminal in X Window | Command Line |
|---|---|---|
| yast2 | Qt | ncurses |
| yast | Ncurses | ncurses |

Table 4-1

In the graphical interface, you can control YaST with the mouse. To start it, select YaST from the main menu (Computer > More Applications > System > YaST). You are asked to enter the root password. See Figure 4-1.

![](img/9129877170834ca9d5fdac5319bf5f12_107_0.png)

Figure 4-1

The YaST dialog appears in Figure 4-2.

To start the ncurses interface of YaST, you can start a terminal emulation from your GNOME desktop by right-clicking on the desktop background and selecting Open Terminal. See Figure 4-3.

Enter su – to get root permissions. After entering the root password, start YaST by entering yast.

![](img/9129877170834ca9d5fdac5319bf5f12_108_0.png)

Figure 4-2

![](img/9129877170834ca9d5fdac5319bf5f12_108_1.png)

Figure 4-3

The ncurses interface is controlled with the keyboard. Press Tab to move from one box to another or to the text buttons. To go back to the previous box, press Shift+Tab. Use the arrow keys to navigate within the box. Mark highlighted menu items by pressing the Spacebar.

To select a menu item, press Enter. You can often press Alt and the highlighted letter to access an item directly.

Except for the controls and the appearance, the graphical mode and the text mode of YaST are identical.

You can list the available YaST modules with the yast -l command or yast --list. To start an individual module, specify its name. For example, you can enter the following to start the software installation module:

```
yast sw_single
```

You can enter the software module name with the yast command or yast2, as in the following:
- `yast sw_single` (text mode)
- `yast2 sw_single` (graphical mode)

![](img/9129877170834ca9d5fdac5319bf5f12_109_0.png)

To install a software package you can also enter **yast -i package.rpm**. The package is installed directly without any dialogs.

To display a list of YaST options, enter one of the following:
- `yast --help`
- `yast -h`

The main dialog of YaST is called the *YaST Control Center*.

On the right side you can access any YaST module available. When you select a category on the left (such as Software or System), the modules in that category are highlighted on the right side.

When you finish making changes with a YaST module, YaST uses backend services such as SuSEConfig (see Objective 3—Understand the Role of SuSEConfig) to implement the changes in the system.

## Objective 2—Become Familiar with YaST Modules

YaST modules are generally quite easy to use and are accompanied by help texts in the left part of the dialogs. You already saw some modules, like the YaST Partitioner, during installation.

This objective will cover the following modules:
- YaST Hardware Information Module
- YaST Date and Time Module
- YaST Language Module
- YaST Keyboard Module

## YaST Hardware Information Module

The YaST Hardware Information module is not used to change any settings. It is used to gather information on the hardware available in the machine. It is invoked by selecting Computer > More Applications > System > YaST > Hardware Information.

After the module gathers the information, the dialog shown in Figure 4-4 appears.

![](img/9129877170834ca9d5fdac5319bf5f12_110_0.png)

Figure 4-4

You can browse the information by expanding the sections of the tree that are of interest to you.

## YaST Date and Time Module

The Date and Time module can be used to change the date and time, the time zone, and whether your hardware clock is adjusted to local time or UTC (Universal Time Coordinated).

The Date and Time module is started by selecting Computer > More Applications > System > YaST > System > Date and Time. The dialog shown in Figure 4-5 appears.

![](img/9129877170834ca9d5fdac5319bf5f12_111_0.png)

Figure 4-5

![](img/9129877170834ca9d5fdac5319bf5f12_111_1.png)

The command-line tools to change the system time and change the hardware clock are **date** and **hwclock**. See the respective manual pages for details on how these are used.

## YaST Language Module

The YaST Language module changes the language settings in the virtual terminals and on the desktop.

The Language module is started by selecting Computer > More Applications > System > YaST > Language. The dialog shown in Figure 4-6 appears.

![](img/9129877170834ca9d5fdac5319bf5f12_112_0.png)

**Figure 4-6**

You can change the Primary Language in the drop-down list in the upper part of the dialog, and adjust the time zone and keyboard settings according to your language choice.

In the lower part it is possible to select secondary languages. If you do that, language-specific packages, such as spell checkers, are installed for those languages as well.

Selecting Accept installs any missing language-specific packages—for the primary and secondary languages—and changes the necessary settings.

For the changes to have effect on the desktop, you must log out and back in again.

## YaST Keyboard Module

The YaST Keyboard module allows you to change the keyboard layout. It is started by selecting **Computer > More Applications > System > YaST > System > Keyboard Layout**. The dialog shown in Figure 4-7 appears.

![](img/9129877170834ca9d5fdac5319bf5f12_113_0.png)

**Figure 4-7**

Select the keyboard layout you want to use; then select OK.

![](img/9129877170834ca9d5fdac5319bf5f12_113_1.png)

A user can also change the keyboard layout for himself in the GNOME Control Center by selecting **Computer > Control Center > Keyboard**.

![](img/9129877170834ca9d5fdac5319bf5f12_114_0.png)

## Exercise 4-1: Get to Know YaST

In this exercise, you use the different user interfaces of YaST and start some YaST modules to do the following:
- Start the graphical user interface of YaST.
- View the `/proc/version` file with the YaST System Log module.
- Set the time and date.
- View the `/proc/version` file with the ncurses user interface of YaST.

## Detailed Steps to Complete This Exercise

- Part I: Start YaST
- Part II: View the Content of a System Log File
- Part III: Change Time
- Part IV: Start the ncurses
- Part V: View the Content of a System File

## Part I: Start YaST

To start YaST, do the following:
1. From the GNOME desktop, open the main menu.
2. Select More Applications.
3. Type ya in the Filter text box.
4. Select the YaST icon to start YaST.
5. Type the root password `n0v3ll` in the appearing dialog; then select Continue or press Enter.
   The YaST Control Center appears.

## Part II: View the Content of a System Log File

To view the content of a system log file, do the following:
1. In the YaST Control Center, select Miscellaneous > View System Log.
2. From the top drop-down list, select /var/log/boot.msg.
3. Close the log window by selecting OK.

## Part III: Change Time and Date

To change time and date, do the following:
1. In the YaST Control Center, select System > Date and Time.
2. Select Change.
3. Type the current time (such as 08:00:00) and the current date (such as 27/05/2007).
