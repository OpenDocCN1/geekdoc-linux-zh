# Selecting Your Desktop

Fluxbox is the default window manager used by Damn Small Linux. DSL also lets you switch to the Joe’s Window Manager (JWM), if you prefer. JWM offers a desktop interface that is somewhat similar to the Microsoft Windows desktop interface. The version of JWM in DSL is a heavily modified and stripped-down version of the original JWM.

You can change window managers by displaying the desktop menu (right-clicking the desktop) and selecting WindowManager, Switch to JWM. You can switch back to Fluxbox from the desktop menu by selecting Exit, Switch to Fluxbox. (Before switching window managers, keep in mind that this action will restart the X Window system and close any applications you have open.)

You can add applications to open when your desktop launches by editing configuration files in the dsl home directory (`/home/ds1`). For example, by editing the `.xinitrc`, you can start up your favorite X programs. You can start non-X programs by editing the `.bash_profile` and then adding it to your `filetool.1st`.

If you need to load additional modules and system-specific required files, you can do so by editing the `/opt/bootlocal.sh` file and then adding it to your `filetool.1st`.

# Managing Icons

Most distributions have the luxury of using prebuilt integrated desktop systems, or even icon management systems, such as Rox (http://rox.sourceforge.net). In keeping with DSL’s “smaller is better” theme, XtDesk icon program was used. The challenge was that, although XtDesk icons were very functional, there were no GUI configuration tools. I created a small Lua/Fltk GUI together with making a few modifications to the XtDesk code to create DSL’s own unique icon management tool.

First, let’s discuss the standard XtDesk editing capabilities. When you right-click an icon, a small pop-up appears. Sometimes, the pop-up contains alternate or related programs to start and the bottom section of the pop-up is labeled Properties. Clicking Properties brings up a screen similar to the one shown in Figure 4-3.

You can move the box cursor and edit any of the icon properties. The MenuCommand1 option is the alternate right-click way to launch the program. The Status option is custom to DSL and should be used for base application. The additional applications called MyDSL extensions should not use the Status field. Usually, this screen is used to manually change X and Y coordinates, change the caption, and so on.