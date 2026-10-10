# 224 Part I ♦ Getting Started

All of the icon names are included in the single array beginning on line 96. The array of names is used to insert icons into the toolbars to be displayed. The GnomeUIInfo array on line 97 is used as a construction location for the toolbar definitions. The GnomeUIInfo struct on line 92 is an entry for an icon item, but it is missing the label and the item name. The GnomeUIInfo struct on line 96 is the standard array terminator.

The while loop beginning on line 118 is executed once for each toolbar created. The inner loop on line 119 is executed once for each icon being inserted into the current toolbar. The call to memcpy() on line 120 copies an icon entry into the array. Then the icon-identifier strings are inserted on lines 122 and 123 (it isn’t required, but in this example, the name of the icon and the label text are the same). The call to memcpy() on line 124 copies the terminator to the next position in the array, making it a valid toolbar definition.

The display sizes of toolbar icons are all the same—that is, every icon on a toolbar expands both horizontally and vertically to match whichever size is the largest. As you can see in Figure 8-13, it is the text of the label that makes some of the icons very wide. To make the display better fit the window, the count of the number of icons added to the toolbar is adjusted on line 127 whenever a name exceeds 12 characters.

Removing the text annotation beneath the icons results in a much smaller display. Figure 8-14 shows the results of removing line 123 of the program, resulting in icons with no text. The figure also shows that every toolbar can be positioned and oriented separately—a toolbar can be docked horizontally on the top or bottom, docked vertically on the left or right, or placed anywhere on the screen in either horizontal or vertical orientation.

![](bbox=[0.18, 0.62, 0.55, 0.93])

# Figure 8-14: Toolbars can be repositioned independently