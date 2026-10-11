
## Cards Subpanel

The following graphic shows the Cards subpanel. In addition to the Install Icon control, it includes the Today control, which opens the Calendar to the current month with current date selected, and the Find Card control, which opens the Address Manager’s Search dialog box.

![](img/256e02a6afce528d264a8d911fa0ff20_278_1.png)

## Files Subpanel

The Files subpanel is one of the more commonly used subpanels of the front panel. It includes the Home Folder control, which opens the Home folder’s window in the File Manager; the StarOffice Work Folder control, which opens the File Manager to the `/Office51/work` folder where StarOffice stores files by default; the Open Floppy and Open CD-ROM controls, which open a floppy disk and CD-ROM window, respectively; the Properties control, which opens the Properties dialog box in which you can determine the attributes of files and directories; Encryption, Compress File, and Archive controls, each of which performs the actions they are named for; and finally, the Find File control, which opens Solaris’s Find utility.

![](img/256e02a6afce528d264a8d911fa0ff20_279_0.png)

## Applications Subpanel

The Applications subpanel is probably the most commonly used subpanel of the front panel because it contains both applications and controls that allow you to customize and work with the CDE desktop in many ways. In addition to the Install Icon control, you will find the Text Note control, which opens a single-file text editor application that stores notes and puts a link to them on your workspace. The Text Editor control opens the text editor, which is more fully described in Chapter 16. The Voice Note control opens the CDE Audio Application, which you can use to record from a microphone or a line to a sound file.

![](img/256e02a6afce528d264a8d911fa0ff20_279_1.png)

Of particular importance is the **Applications** control, which opens the Application Manager window shown in Figure 7.13. The reason the **Applications** control is important is that the Application Manager program folder window contains many desktop, system, and administrative programs and controls that you can use to modify your system behavior. Programs represented in this folder are both CDE and OpenWindows applications and actions. In fact, many of the controls on the front panel and its subpanels are found in the **Application Manager** folder and in the folders it contains. When you need to perform a task using a program or utility that you can't find on any of the menus, the **Application Manager** folder is a good place to start looking. Among the important folders you find there are the `Desktop_Apps`, `Desktop_Controls`, `Desktop_Tools`, `Information`, `OpenWindows`, and `System_Admin` folders. It's a good idea to open these folders and study their contents when familiarizing yourself with Solaris. You will also probably find a few controls therein that you may want to add to your front panel or its various subpanels. In addition to opening the Application Manager with this subpanel control, you can also use the **Applications** submenu of the Workspace Menu.

**FIGURE 7.13**
**The Application Manager program folder**

![](img/256e02a6afce528d264a8d911fa0ff20_280_0.png)

## Mail Subpanel

The Mail subpanel is shown in the following graphic. This subpanel offers you two unique controls: the **Mail** control, which opens the Mail utility, and the **Suggestion Box** control, which creates new mail to `Solaris8_Suggestion_Box@eng.sun.com`.

![](img/256e02a6afce528d264a8d911fa0ff20_280_1.png)

## Printers Subpanel

The following graphic shows the Personal Printers subpanel. This subpanel also has only two other controls besides the Install Icon control: the Default control, which opens the default printer's Printer Jobs queue, and the Print Manager control, which opens the Printer Manager dialog box.

![](img/256e02a6afce528d264a8d911fa0ff20_281_0.png)

## Tools Subpanel

The Tools subpanel menu opens from just above the Desktop Controls control. This subpanel has a number of different tools. Using the Desktop Controls control, you can open a folder containing tools you can use to modify the way your desktop appears. For more information, see “Desktop Controls” later in this chapter. The CDE Error Log control opens the Watch Errors window with a display of system error messages.

![](img/256e02a6afce528d264a8d911fa0ff20_281_1.png)

The Add Item to Menu control opens the Add Item to Workspace Menu dialog box (see Figure 7.14), through which you can add a file or folder to the `$HOME/.dt/wsmenu` directory. The Customize Workspace Menu control opens the `$HOME/.dt/wsmenu` folder, which contains symbolic links to the programs and actions that are in all of the subpanel menus, as shown in Figure 7.15. You can drag and drop additional actions and links into each of these folders and use the `/wsmenu` directory as a means of organizing all of your subpanels.

**FIGURE 7.14**
The Add Item to Workspace Menu dialog box

![](img/256e02a6afce528d264a8d911fa0ff20_282_0.png)

**FIGURE 7.15**
The Workspace Menu window

![](img/256e02a6afce528d264a8d911fa0ff20_282_1.png)

**NOTE** When you drag a file or directory into the wsmenu directory using the Customize Workspace Menu dialog box, that file or directory is moved (not copied) into the wsmenu directory. To create a symbolic link in the wsmenu directory, hold down the Shift and Ctrl keys before performing the drag-and-drop operation.

The Find Process control opens the Process Manager, which shows you the details of all of the processes running on your system. You can use this window to debug your system, to kill an errant process, and to perform many other tasks. Finally, the last control on the Tools subpanel is the Hotkey Editor control. It opens the Hotkey Editor, which you can use to define keystroke macros that you want to use on your system. This utility is described more fully in the section “The Hotkey Editor” later in this chapter.

## Hosts Subpanel

The Hosts subpanel menu is shown in the following graphic. It contains the Performance control, which is another way to open the Performance Meter window; the This Host control, which opens a terminal window; and the System Info control, which opens the Workstation Information dialog box.

![](img/256e02a6afce528d264a8d911fa0ff20_283_0.png)

The Workstation Information dialog box, shown in Figure 7.16, shows you details about the system that you have logged in to, either the local workstation or server or a remote system. The Hosts subpanel menu also includes the Console control, which opens a console window, and the Find Host control, which opens the search utility for the Address Manager. You can use the Address Manager to find workstations and servers on the network or Internet by name or address.

![](img/256e02a6afce528d264a8d911fa0ff20_284_0.png)

## Help Subpanel

The Help Manager control opens the Help subpanel menu shown in the following graphic. This subpanel contains a number of controls for accessing the different kinds of help that is available on your system. (Chapter 3 described the various types of help in detail.) The Help Manager control duplicates the action of the front panel control by opening the Help Manager in the Help Viewer. The SunSolve Online and Solaris Support controls open your Web browser to those Sun sites. The Information control opens the Application Manager Information folder with links to the AnswerBook2 and Sample Bookmarks. Beginning users will find the Desktop Introduction and Front Panel Help controls useful; they open the Help Viewer with information on these basic tasks and with documentation of the front panel. The On Item Help control is used for context-sensitive help; when you click this control, your cursor turns into a question mark. Click on any control to open the Help Viewer to that topic.
