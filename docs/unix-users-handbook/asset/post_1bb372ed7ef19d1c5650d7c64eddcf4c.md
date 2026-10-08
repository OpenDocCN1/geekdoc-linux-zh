
typically the image plane, is designated as 0. Note also the inclusion of workspace names (One, Two, Three, Four, Five, and Six) in the six title resource specifications.

These changes can be added to the **sys.resources** file, which is discussed in detail in “Advanced Topics” later in this chapter. These changes can also be made by use of the **EditResources** action to insert the new resource lines into each user’s **RESOURCE_MANAGER** property and then restart the workspace manager.

The obvious disadvantage is that you have to physically go to each user’s work area and take over the machine for a few minutes. However, on the plus side, the changes are immediate and are automatically saved in the correct **dt.resources** for users who restore their current session. You also avoid having your changes overwritten, which could happen if you modify the right **dt.resources** file at the wrong time, while the user is still logged in.

### Modifying Things in Slideup Subpanels

Subpanels are defined in **dtwm.fp** after the front panel and front-panel control definitions. To associate a subpanel with a front panel control button, the front-panel control name is listed as the container name in the subpanel definition.

> Note: /etc/dt is where global changes are made. $HOME/.dt is where local or individual user changes are made.

- To add a slideup subpanel to the front panel follow these steps:
- Copy the file /usr/dt/appconfig/types/C/dtwm.fp to /etc/dt/appconfig/types/C/dtwm.fp or to $HOME/.dt/types/dtwm.fp.
- Decide which control button with which the slideup is to be associated.
- Create the subpanel definition file in dtwm.fp. This will take the following form:

```
SUBPANEL SubPanelName
{
CONTAINER_NAME AssociatedFrontPanelControlButton
TITLE SubPanelTitle
}
```

- Create subpanel control definitions for the subpanel. These will take the following form:

```
CONTROL ControlName
{
TYPE icon
CONTAINER_NAME SubPanelName
CONTAINER_TYPE SUBPANEL
ICON BitmapName
PUSH_ACTION ActionName
}
```

As with front panel control buttons, it’s easier to copy and modify an existing subpanel file than to start from scratch.

## Changing the Default Printer Name Display

We can make an easy change to one of the slideup subpanels. If we pop up the Personal Printers subpanel, it shows that we have a default printer configured, but not the name of it. Let’s go back into the front panel file, **dtwm.fp**, and change that.

- Bring up your favorite editor, such as **dtpad** or **vi**, and edit **/$HOME/.dt/types/dtwm.fp**.

![](img/75f39fc91296b889c0653851accdfd46_250_0.png)

- Scroll down to **CONTROL Printer**. You’ll see that the **LABEL** is Default. **Change** or add to that the name of your default printer. My printer is called **a464**.

**LABEL Default - a464**

- **Save the file** and **restart Workspace Manager**. Position the mouse over a blank area on your workspace and press the right mouse button. Select Restart Workspace Manager. On Solaris, press the right mouse button to bring up the Customized Workspace Menu. From here, select Windows, where you’ll find the Restart Workspace Manager key.

Pop up the Personal Printers subpanel and now we can see what our default printer really is. Of course, if we change the default, we’ll have to change the front panel again. But we know how to do that now, don’t we! Figure 4-5 shows the Front Panel.

![](img/75f39fc91296b889c0653851accdfd46_251_0.png)

## Front Panel Animation

Animation for front-panel or slideup-subpanel drop zones is created by displaying a progressive series of bitmaps. By convention, the bitmaps are in `/usr/dt/appconfig/icons`. The list of bitmaps to display is contained in animation definitions at the end of `dtwm.fp`.

To create an animation sequence for a drop zone:

- Create a progressive series of bitmaps.
- Add a list of these bitmap files to the appropriate configuration file using the following syntax:

```
ANIMATION AnimationName
{
   bitmap0
   bitmap1
   bitmap2
   bitmap3
   bitmap4
   bitmap5
}
```

- Add a line to the appropriate control definition using the syntax:

```
DROP_ANIMATION AnimationName
```

## Adding Things to the Workspace Menu

The workspace menu is defined in the sys.dtwmrc file. As mentioned in the overview of the front panel for Solaris, the Workspace Menu is accessed by placing the mouse over a blank area of the desktop and pressing the right mouse key. Where AIX and HP-UX come with a generic menu, Solaris has incorporated the front-panel and subpanel actions into the Workspace Menu as another way to access these actions. However, we can create customized Workspace Menu for all three systems using the left mouse key to access it. We'll be doing this task next.

A workspace menu can contain frequently used commands and applications. The customized menu is usually accessed by pressing the left mouse button, which pops up the menu for viewing and selection. A workspace menu comes in handy for those who have a set number of things they do regularly. For instance, a programmer who uses C++, vi, and isql may have a menu with those items, or a system administrator may have a menu with df, ps -ef, and netstat on it. Or those on an expansive network may want a menu of system logins.

For one or two changes, you can modify the existing workspace menu. For major changes, it's probably easier to insert an entirely new menu definition in sys.dtwmrc.

A menu definition has the following syntax:

```
Menu MenuName
{
"Menu Name" f.title
"Frame" f.exec /nfs/systeml/usr/frame/bin/maker
"Second Item" action
"Third Item" action
}
```

![](img/75f39fc91296b889c0653851accdfd46_253_0.png)

![](img/75f39fc91296b889c0653851accdfd46_253_1.png)

![](img/75f39fc91296b889c0653851accdfd46_253_2.png)

![](img/75f39fc91296b889c0653851accdfd46_253_3.png)

The first line specifies the menu name, following the keyword Menu. The lines between the curly braces list the items that appear in the menu in their order of appearance; thus the first line is the title as designated by the function f.title. The second line is an example of a definition that would start FrameMaker from a remote application server in a distributed environment. Numerous other functions exist, approximately 45 in all. For a complete list, see the dtwmrc (4) man page.

For users to display the menu, you need to bind the menu definition to a mouse button and a screen location using the action f.menu MenuName. For example, if your users want to post the menu by pressing mouse button 3 when the pointer is on the workspace background, you would insert the following line in the Mouse Button Bindings Description section at the end of sys.dtwmrc:

```
<Btn3Down> root f.menu MenuName
```

(Actually, it would be easier to modify the line that's already there by exchanging MenuName for DtRootMenu on the second line.)

Now, we'll create a simple menu. Our menu is going to include running FrameMaker, running the vi editor, and logging into a remote system.

- First we need a copy of the /usr/dt/config/C/sys.dtwmrc file to /etc/dt/config/C:

```
cp /usr/dt/config/C/sys.dtwmrc /etc/dt/config/C/sys.dtwmrc
```

If we were going to make this a local change for one user only, it would be copied to $HOME/.dt and renamed **dtwmrc**. For the admin1 user, that would be /home/admin1/.dt/dtwmrc or on Solaris in /home/admin1/.dt/C/dtwmrc.

- Go into our favorite editor and **modify the file**. We’re going to add our new menu just after the DtRootMenu entry, which we see on our system as the left mouse button’s “Workspace Menu.” Add the following:

```
Menu AdminMenu
{
	“Admin1’s Menu”			f.title
	“Frame Maker”			f.exec “/nfs/system1/usr/frame/bin/maker”
	“VI Editor”			f.exec “xterm -e /usr/bin/vi”
	“Login systemA”			f.exec “xterm -geometry 80x50+830+0 -sl 200 -bg DarkOrchid4 -fg white -n SYSTEMA -T SYSTEMA -e remsh systemA &”
}
```

The **f.title** function shows that this is the menu title. **f.exec** means to execute the following string. Notice that FrameMaker does not need a terminal window, because it uses its own, whereas vi and the login both need a terminal window in which to run. Also, I embellished on the xterm for the login, making the terminal window very large, with lots of terminal memory, and using specific colors.

Now, let’s restart the Workspace Manager and try out our new menu.

- Position the mouse over a blank area on the workspace and press the left mouse button. Select **Restart Workspace Manager**.
