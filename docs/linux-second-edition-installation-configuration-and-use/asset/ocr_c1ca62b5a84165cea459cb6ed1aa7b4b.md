# GIMP FOR ADVANCED USERS 703

If you work with large images and allow many Undo levels, the requirement of the Gimp swap file quickly rises to the stars! Several hundreds of megabytes by no means. At the same time, the speed slows down beyond endurance (unless you do not have a huge amount of RAM, that is, 256 Mbytes and more).

Please also note that in the event of a crash, Gimp does not remove the swap file. Thus, if your hard disk is unexpectedly full, check the Gimp swap file directory.

# Redefining keyboard shortcuts

Many commands have their keyboard shortcuts which are displayed in the menu text. Nothing is easier than using a different shortcut instead, or assigning a new shortcut in the first place. Begin the menu selection with the mouse, letting the mouse point to the menu command, without concluding the selection with a mouse click. Then press the required key combination – done. It could not be simpler. (The modified keyboard shortcuts are stored in the local file menrc.)

# Setting the menu font size

In the default configuration, Gimp displays its menus in a tiny font. This can be remedied by modifying "/.gimp/gtkrc (local) or /usr/share/gimp/gtkrc (global). The following lines help you to obtain a font size of 17 points in menus and dialogs.

```
# configuration file gtkrc
style "ruler"
  font = "--adobe-helvetica-medium-r-normal--17-*" 
  style "default"
  font = "--adobe-helvetica-medium-r-normal--17-*" 
  widget_class "*Ruler*" style "ruler"
  widget_class "**" style "default"
```