```
Menu AdminMenu
{
    "Admin1's Menu"         f.title
    "Frame Maker"           f.exec "/nfs/system1/usr/frame/bin/maker"
    "VI Editor"             f.exec "xterm -e /usr/bin/vi"
    "Login systemA"         f.exec "xterm -geometry 80x50+830+-0 -sl 200 -bg DarkOrchid4 -fg white -n SYSTEMA -T SYSTEMA -c remsh systemA &"
```

The **f.title** function shows that this is the menu title. **f.exec** means to execute the following string. Notice that FrameMaker does not need a terminal window because it uses its own, whereas **vi** and the **login** both need a terminal window in which to run. Also, I embellished on the **xterm** for the login, making the terminal window very large, with lots of terminal memory and using specific colors.

Now, let's restart the Workspace Manager and try out our new menu:

+   3.  Position the mouse over a blank area on the workspace and press the left mouse button. Select **Restart Workspace Manager**.

Creating pull-down menus is easy and can easily be expanded by adding submenus to the menu. Just use the function **f.menu** followed by the menu name. Add the following just after "Admin1's Menu":

```
"Work Menu"         f.menu  WorkMenu"
```

And then after the } from the Menu AdminMenu section, add:

```
Menu WorkMenu
{
    .
}
```

Performing these advanced functions really isn't so hard. The hardest part is remembering which directories to put the files in: **/etc/dt** for global changes or **$HOME/.dt** for individual changes.