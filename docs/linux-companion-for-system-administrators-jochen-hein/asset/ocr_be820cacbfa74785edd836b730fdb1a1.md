# 6.4.2 The fwwm modules

Many functions required by some users need large amounts of memory which can be saved without causing problems for other users. fwwm supports this via the use of modules that carry out special functions.

+   - GoodStuff
This module generates an icon bar which allows frequently used programs to be started with a click of the mouse. This bar can be easily configured for each user and can be positioned anywhere on the screen. To make the bar appear, fwwm must be started together with this module.

+   - FwmAudio
This module allows you to associate sounds to specific window actions, for example, every time the close button is selected, you hear the sound of a breaking glass pane (provided a sound driver pulse hardware exists and is activated).

+   - FwmBack
Allows you to associate each desktop to a separate screen background and display it when desktops are changed. Any available program can be used for this purpose, for example xv, xsetroot, xpmroot, hearth, and so on.

+   - FwmBanner
Shows the fwwm logo in the middle of the screen for five seconds. Can also be called from the command line.

+   - FwmIconBox
Manages a box containing the icons of the started programs.

+   - FwmPager
Allows to switch between the virtual desktops by means of a simple click in an overview window. This window can also be integrated into the icon bar of GoodStuff.

+   - FwmSave
Allows the layouts (sizes and positions) of the active applications to be stored in the file ~/new.xinitrc. Obviously, this file must then be used by ~/.session or ~/.xinitrc.

+   - FwmWinList
Displays a list of open windows. A window can be activated by clicking on the corresponding entry in this list.