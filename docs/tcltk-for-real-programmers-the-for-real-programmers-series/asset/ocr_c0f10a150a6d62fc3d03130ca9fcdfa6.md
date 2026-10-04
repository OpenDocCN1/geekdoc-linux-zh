# Chapter 9. The canvas Widget, Images, and Events

```
.c move star $xoff $yoff
update;
```

# Script Output

| Pass 1 | Pass 3 | Pass 5 | Pass 7 | Pass 9 |

Tk stores the location of items in floating-point coordinates; thus the bouncing star doesn't completely stop until the x and y velocities fall below the precision of the floating-point library on your computer. The star will just move more and more slowly until you get bored and abort the program.

# 9.4.4 Finding Items, Raising and Lowering Items

The canvas can be searched for items that meet certain criteria, such as their position in the display list, their location on the canvas, or their tags. The canvas widget subcommand that searches a canvas is the find subcommand. It will return a list of unique IDs for the items that match its search criteria. The list is always returned in the order in which the items appear in the display list, the first item displayed (the bottom if there are overlapping items) first, etc.

The items in a canvas widget are stored in a display list. The items are rendered in the order in which they appear in the list, thus items that appear later in the list cover items that appear earlier in the list.

An item's position in the display list can be changed with the raise and lower subcommands.

```
Syntax: canvasName raise tagOrId ?aboveTagId?
```

+   raise Move the identified item to a later position in the display list, making it display above other items.