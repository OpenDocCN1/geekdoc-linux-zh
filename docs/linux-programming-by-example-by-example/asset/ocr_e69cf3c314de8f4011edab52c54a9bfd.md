# Output

![](bbox=[0.09, 0.18, 0.91, 0.55])

The first thing this code does is create a static text array that will become the menu, as well as several other variables it will use. It uses the keypad function to interpret function and cursor keys. Next, it steps through the static text array, peeling off each string and adding it to the ITEM vector items. To create the menu, you must pass items to new_menu, which returns a pointer to m ymenu that points to a properly initialized menu structure. The

```
```c
set_menu_format call
set_menu_format(mymenu, 5, 1);
```
```

creates a menu that is five rows long and one column wide, so that the program can demonstrate how to move up and down the menu. After the menu has been created and formatted, post_menu associates m ymenu with s t d s c r and handles all the refreshing and updating. Finally, refreshing the screen makes the menu visible. At this point, you can scroll up and down the menu using the up and down arrow keys and the Page Up and Page Down keys.

The workhorse of the sample program is the while loop. It takes input from the keyboard and passes it to the menu_driver function, which handles all the menu manipulation. Pressing the down arrow key, for example, generates a KEY_DOWN signal that menu_driver receives as a REQ_DOWN_ITEM, thus telling menu_driver to highlight the next menu item down on the menu.

unpost_menu, free_menu, and the for loop that frees the individual menu items return allocated resources to the kernel. At last, the program terminates with the calls to app_exit and exit.