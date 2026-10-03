After you define an action, you can use that action in the desktop user interface to simplify tasks. The desktop provides the ability to attach user interface components such as icons, Front Panel controls, and menu items to actions. Each of these icons performs an action when the icon is double-clicked.

Another common use of actions is in menus. Data files usually have actions in their selected menu in File Manager. For example, XWD files (files with names ending in .xwd or .wd) have an Open action that displays the screen image when you run the Xwd action.

Actions and data types are powerful components for integrating applications into the desktop. They provide a way to create a user interface for starting applications and manipulating data files. For more information on creating actions, see the Solaris CDE Advanced User’s and System Administrator’s Guide.

# THE APPLICATION MANAGER

Application Manager is the desktop container displaying applications available to users. It is selected from the Applications pop-up menu located on the Front Panel, shown earlier in Figure B.6.

When initially opened, the Application Manager window displays the top-level directory of the Application Manager. User interaction with the Application Manager is similar to the use of the File Manager, except that the Application Manager contains executable modules. The user launches the Application Manager from an icon on the Front Panel, opening the window shown in Figure B.9.

![](bbox=[0.48, 0.1, 0.8, 0.17])

FIGURE B.9
The Application Manager window.

Programs and icons can be installed in the Application Manager by the system administrator, and can be pushed out to other workstations as part of the installation process. By default, the Application Manager comes preconfigured to include several utilities and programs (see Figure B.9). Each of these utilities is located in a directory, which—with its contents—is called an application group. Application groups provided with the default desktop are described in Table B.6.

# TABLE B.6

# APPLICATION GROUPS

| Group | Description |
|---|---|
| Desktop_Apps | Desktop applications such as File Manager, Style Manager, and Calculator. |
| Desktop_Tools | Desktop administration and operating system tools such as User Registration, Reload Application, vi text editor, and Check Spelling. |
| Information | Icons representing frequently used help topics. |
| System_Admin | Tools used by system administrators. |
| Desktop Controls | Tools to set your CDE environment, such as mouse behavior, desktop fonts, screen saver, and window behavior. |
| OpenWindows | Group that contains several OpenWindows-style actions, such as the mail tool and File Manager. |