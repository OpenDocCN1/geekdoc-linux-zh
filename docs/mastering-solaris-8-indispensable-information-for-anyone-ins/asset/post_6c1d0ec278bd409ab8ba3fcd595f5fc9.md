
# Trash Subpanel

The Trash control opens the Trash subpanel. This subpanel contains the Trash control you can use to open the Trash Can folder and the Empty Trash Can control for shredding all items in your Trash Can folder.

![](img/256e02a6afce528d264a8d911fa0ff20_285_0.png)

![](img/256e02a6afce528d264a8d911fa0ff20_285_1.png)

# Modifying the Front Panel

You can add or delete a subpanel by right-clicking on a control and selecting the Add Subpanel or Delete Subpanel command from the pop-up menu. The following graphic shows the pop-up menu for the File Manager control. You’ll notice that you can also use the Move Left and Move Right commands to move a control’s icon around in the subpanel. Note that you can’t move an icon that is at the left or right front panel border, nor can you move an icon into the Workspace panel. When you issue the Add Icon command in the pop-up menu, you add a new blank control to the front panel to the left of the pop-up menu; this control doesn’t modify the icon of any of the existing controls. To provide an action to the blank control, you can drag and drop an icon from the desktop to it. The commands you see in the pop-up menus that you open on the front panel depend upon whether a menu was opened over an existing control or not.

![](img/256e02a6afce528d264a8d911fa0ff20_285_2.png)

![](img/256e02a6afce528d264a8d911fa0ff20_285_3.png)

![](img/256e02a6afce528d264a8d911fa0ff20_286_0.png)

When you add a new control to the front panel, that control is a blank embossed button, like the icon next to the Install Icon control you see at the top of every subpanel. To give that control a function, you must drag and drop an executable file (program icon), a document, or some other system content from the desktop onto the icon. If you want to delete a front panel icon by selecting the Delete Icon command from that control’s pop-up menu, then Solaris will display the Workspace Manager Delete Icon dialog box. If you delete a front panel icon, you also delete any application that the control is linked to. The application may no longer exist or function. To restore your front panel to the state it was in when Solaris was first installed, double-click the Restore Front Panel application in the Desktop_Tools-Extras application group.

When you want to add an application, file, or action to the front panel, you use the Add Icon command on the pop-up menu of a control or the front panel itself. That action adds the Install Icon control to the front panel. As you have already seen, each subpanel contains the Install Icon control as its top control. To enable a new control, drag and drop the following onto the Install Icon control:

- An executable file of a program
- A folder icon from a File Manager
- A file of any kind
- A script or action

# Actions

An action is a scripted command that is represented by an action icon in the CDE. With an action, you can open files, launch applications, modify the file structure, print, or execute any command that you can enter from the command line. Given that only a single command-line statement can be used, actions aren't really programs, although they can certainly be program calls. The nice thing about actions is that you can create them graphically using the Create Action control found in the **Desktop_Apps** folder of the Application Manager, and the actions that you create can be added to any folder or to the front panel as a control. You can also open the Create Action window by invoking it from the command line using the **dtcreate** command.

To create an action, do the following:

- Open the Applications subpanel on the front panel and click the **Applications control**. The Application Manager folder opens.
- Double-click the **Desktop_Apps** folder, then double-click the Create Action control (shown here).

![](img/256e02a6afce528d264a8d911fa0ff20_287_0.png)

- When the Create Action dialog box opens (shown in Figure 7.17 in Advanced mode), enter a name in the **Action Name** text box. That name will be attached to the icon you create for the action. No spaces are allowed in an action name.
- Click the **Find Set** button to open the Find Set dialog box and select an icon for your action. Figure 7.18 shows the Find Set dialog box. You can also use the **Edit Icon** button to open the Icon Editor (Figure 7.19) and modify the action's icon.

An action icon is part of a registration package that is created when the action is specified, and its integration with the desktop is managed by **dtappintegrate**. Icon image files are located in the `app_root/dt/appconfig/icons/language` folder. When specifying an action stored in this folder, you should use the base name of the action, which is the action name minus all of the suffixes that are appended to it (e.g., `myaction` replaces `myaction.m.pm`).

- In the **Command When Action Is Opened** text box (in the Find Set dialog box), enter any command that you can enter from the command line or enter the full path name of any executable file or shell script.

### FIGURE 7.17

The Create Action window, shown here in Advanced mode, is where you create actions and specify their properties.

![](img/256e02a6afce528d264a8d911fa0ff20_288_0.png)

- In the Help Text for Action Icon text box, enter the text you want to appear when a cursor is over the icon you create.
- Select the window type from the pop-up menu: the default, Graphical (X-Window), runs an application in its own window; Terminal (Auto-Close) runs an application in a terminal window and the window closes as soon as the application completes its action; and Terminal (Manual Close) runs an application in a terminal window and requires a user to give an **exit** command to close the application.
- If you want specific data types to work with this icon, select the Only Above List radio button in the Droplable Datatypes option group, then click the Add button to add the data types that will work with your action.
- Select the Save command from the File menu and the action is saved to your home folder.
- Double-click an action to test its operation (recommended).

### FIGURE 7.18

Use the Find Set dialog box to specify the icon used for an action.

![](img/256e02a6afce528d264a8d911fa0ff20_289_0.png)

### FIGURE 7.19

The Icon Editor

![](img/256e02a6afce528d264a8d911fa0ff20_289_1.png)

If in Step 5 you use for an action a command that requires a filename, such as `1p <filename>` or `diff <file1name1> <file1name2>`, then use a `<var>` variable in place of the filename, as in `1p $1` or `diff $1 $2`. When you create an action and place it in the front panel, it will then serve as a drop zone for files that you drag and drop onto it. Thus you can print the file `memo1` by dragging it onto the action specifying the line printer command, and you can run the file difference command by first dragging the `memo1` file and then the `memo2` file onto the action specifying that command. You can also pass a command to a shell in step 5 by specifying the shell and the command, as in this example:

```bash
/bin/sh -c 'ps | 1p'
```

Installing an action is easy once you have created it. To install an action, simply click and drag it onto the Install Icon control on the menu in which you wish the action to appear.

> TIP If you create a lot of actions, you may find that it makes sense to group them into a new subpanel that you create for that purpose. Create a new My Actions or Personal Applications subpanel by right-clicking the front panel and selecting the Add Icon command from the pop-up menu. Then, after you install a control (the Create Action control would be a good choice), right-click the new front panel control and select the Add Subpanel command.

Double-click the action icon on your desktop if you want to perform the action it represents. If you want to examine the code for an action, open the `/.dt/types` folder and double-click the action’s definition file. The `/.dt` folder is a hidden folder in your root directory, so use the Show Hidden Objects command to view it. When you double-click an action file in the `/.dt/types` folder, you see the definition appear in the text editor, as shown in Figure 7.20. The action opened the oclock application in an X window.

> TIP The Hotkey Editor contains several default hotkeys that change your current workspace. Those hotkey keystrokes include Alt+Left, which moves you to the previous workspace, and Alt+Right, which moves you to the next workspace (these two take effect everywhere, which means they work in all programs as well as on the desktop). The default hotkeys that take effect on the desktop are Left (previous workspace), Right (next workspace), SunAgain (packs icons) and SunUndo (refreshes all windows). See “The Hotkey Editor” later in this chapter for more information.
