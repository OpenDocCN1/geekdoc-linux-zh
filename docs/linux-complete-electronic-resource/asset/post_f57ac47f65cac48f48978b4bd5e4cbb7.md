
for Events. If you select Enable Sound for GNOME you will make sure that GNOME's sound engine (ESD) will be launched every session of GNOME you run. Enable Sound for Events will launch any sound files you have set in the Sound Events tab when those events occur. With these two items enabled you will utilize GNOME's session management which will remember your sound settings whenever you log in or out.

### Sound Events
This tab allows you to navigate through the sound events in GNOME and change their sounds.

To change a sound associated with a GNOME event, select the event in the hierarchical list on the left and press the Browse button to find a sound file on your system that you wish to associate with that event. Once you have found a sound file, press the Play button to test the sound and see if you like it enough to hear it every time the event occurs.

![](img/a3584dae761d2e3abed8bf40d7637389_635_0.png)

FIGURE 15.35: The Sound capplet

## Peripherals

The capplets in this section of the Control Center will help you configure hardware input devices including keyboard and mouse properties.

### The Keyboard Properties Capplet
There are currently two settings for the keyboard in the Keyboard Properties capplet (see Figure 15.56): Auto-repeat and Keyboard Click. You may change the properties of Auto-repeat and Keyboard Click. Auto-repeat enables you to hold a key down and have it repeat the character at the rate and delay you set in this capplet. Keyboard Click enables a small click sound to play at each key press.

![](img/a3584dae761d2e3abed8bf40d7637389_636_0.png)

**FIGURE 15.56:** The Keyboard Properties capplet

### The Mouse Properties Capplet
The Mouse Properties capplet (see Figure 15.57) allows you to change between left- and right-handed mouse buttons and define the Acceleration and Threshold properties.

The Acceleration setting allows you to change the speed the mouse moves across the screen in relation to the movement of the mouse on your mouse pad. The Threshold setting allows you to set the speed at which you have to move your mouse before it starts the acceleration speed you have defined in the Acceleration setting.

![](img/a3584dae761d2e3abed8bf40d7637389_637_0.png)

FIGURE 15.37: The Mouse Properties capplet

## Session Manager

The Session Manager capplet (see Figure 15.38) allows you to control the GNOME Session Management. This includes which programs start up, how you save your GNOME configuration, and how you log out. You can find out more information about Session Management in “A Word about Session Management” section later in this chapter.

- **Prompt on Logout** This first option allows you to disable the prompt when logging out
- **Automatically Save Changes to Session** This will make the Session Management always save changes made to your GNOME session when you log out.
- **Non-Session-Managed Startup Programs** This allows you to start non-session-managed applications whenever you start a GNOME session.

![](img/a3584dae761d2e3abed8bf40d7637389_637_1.png)

**NOTE** Programs that are not GNOME-compliant are not session-managed so you do not need to put GNOME applications in here; you can simply leave them running and save the current session when you log out.

![](img/a3584dae761d2e3abed8bf40d7637389_638_0.png)

FIGURE 15.38: The Session Manager capplet

If you wish to add a new program to the Non-Session-Managed Startup Programs list, press the Add button. This will launch a simple dialog box that allows you to specify the command to launch the application and what priority it will receive.

The priority for most applications you wish to start is 50. If you have an application that needs to be started before other applications, such as a window manager, set the priority to a lower number.

**NOTE**
This option is for advanced users. Unless you are familiar with the Priority settings you should keep your applications running with a priority of 50.

**Browse Currently Running Programs** This allows you to see what applications are currently running. You may shut down those applications if you wish to and those applications will be removed from your GNOME session. The applications in this list are mostly higher-level applications and should not be shut down. However, if there are parts of GNOME that you do not wish to have, such as the Panel, this is where you would shut it down for now and your next GNOME session.

## User Interface Options

The User Interface Options allows you to change the appearance of applications that are GNOME-compliant. You may recognize these applications as ones that are preinstalled with GNOME or ones that say they are built with GTK (the GIMP Toolkit).

### Application Defaults Capplet
The Application Defaults capplet (see Figure 15.39) allows you to change certain user interface aspects of your GNOME-compliant applications.

**NOTE**
Although this capplet gives you great control over the look and feel of your applications, you should consider these tools for advanced use only.

1. **Can Detach and Move Toolbars** By default toolbars in GNOME applications may be dragged from their usual location and placed anywhere within the application or desktop. If you do not wish to use this feature, you may turn it off.
2. **Can Detach and Move Menubars** By default, menubars in GNOME applications may be dragged from their usual location and placed anywhere within the application or desktop. If you do not wish to use this feature, you may turn it off.
3. **Menubars Have Relieved Borders** By default, menubars have relieved borders. If you do not like this look, you may turn this feature off.
4. **Toolbars Have Relieved Borders** By default, toolbars have relieved borders. If you do not like this look, you may turn this feature off.

![](img/a3584dae761d2e3abed8bf40d7637389_640_0.png)

FIGURE 15.39: Applications Defaults capplet

**Toolbar Buttons Have Relieved Borders** By default toolbar buttons do not have relieved borders in their natural state. They do, however, change when the mouse is over them. If you wish them to be relieved at all times, you may turn on this feature.

**Toolbars Have Line Separators** By default, toolbar buttons have small line separators between them. If you do not wish to have the line separators, you may turn this feature off.

**Toolbars Have Text Labels** By default, toolbar buttons have images and text to identify them. If you are familiar with the buttons and do not need the text, you may turn on this feature.

**Statusbar in Interactive When Possible** Some applications can have the status bar at the bottom become separated into its own window. If you would like to have those applications separate the status bar into another window, you may turn on this option.

**Statusbar Progress Meter on Right** Some applications have progress meters in their statusbars. By default, these progress meters are on the right side of the statusbar. If you wish them to be on the left, you may turn off this feature.

**Dialog Buttons Have Icons** Some dialog buttons (for example the OK button) can have icons on them. By default, the applications that provide this have the icons turned on. If you wish not to see them, you may turn off this feature.

**Menu Items Have Icons** Some menu items in applications will have icons. If you wish not to see these icons in applications that use them, you may turn off this feature.

### The Dialogs Capplet
The Dialogs capplet (see Figure 15.40) allows you to change the default settings for dialog boxes in GNOME-compliant applications. A dialog box is a window that is launched by an application to help perform a task needed by that application. An example of a dialog box is a Print dialog box that appears when you press a Print button. The dialog box allows you to set print options and start the print process. The Dialogs capplet will allow you to change the following options:

![](img/a3584dae761d2e3abed8bf40d7637389_641_0.png)

**FIGURE 15.40:** The Dialog capplet

**Dialog Buttons** Choose to use the default buttons, to spread the buttons out, to put buttons on the edges, to put the buttons on the left with left justify, and to put buttons on the right with right justify.
