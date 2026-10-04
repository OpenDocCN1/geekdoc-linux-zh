# Chapter 9. The canvas Widget, Images, and Events

The *bind* command links scripts to the events that occur on graphic items such as widgets or displayed items in a canvas or text widget. Events include mouse motion, button clicks, key presses, and window manager events such as refresh, iconify, or resize.

After we've discussed the *canvas* and *bind* command, I'll show you how to use them to create a toolbar widget similar to the ones in MS-Windows and Netscape.

# 9.1 Overview of the canvas Widget

Your application may create one or more canvas widgets and map them to the display with any of the layout managers *pack, grid,* or *place*. The canvas owns all items that are drawn on it. These items are maintained in a display list and their position in that list determines which items will be drawn on top of others. The order in which items are displayed can be modified.

# 9.1.1 Identifiers and Tags

When an item is created on a canvas, a unique numeric identifier is returned for that item. The item can always be identified and manipulated by referencing that unique number.

You can also attach a tag to an item. A tag is an alphanumeric string that can be used to group canvas items. A single tag can be attached to multiple items, and multiple tags can be attached to a single item.

A set of items that share a tag can be identified as a group by that tag. For example, if you composed a blueprint of a house, you could tag all of the plumbing with plumbing and then tag the hot water pipes with hot, the cold water pipes with cold, and the drains with drain. You could highlight all of the plumbing with a command like:

```
$blueprint configure plumbing -outline red
```

272