in the console and X to re-map other keys (such as F11 and F12), or key combinations (such as Fn+Ctrl and Fn+Option), to the middle and right mouse buttons. For example, if you have a one-button USB mouse, you can use the following script to map the middle and right mouse buttons to your keyboard's F11 and F12 keys:

```
```sh
#!/bin/sh
echo "1" > /proc/sys/dev/mac_hid/mouse_button_emulation
echo "87" > /proc/sys/dev/mac_hid/mouse_button2_keycode
echo "88" > /proc/sys/dev/mac_hid/mouse_button3_keycode
```
```

The traditional mouse buttons are labeled 1, 2, and 3. The left mouse button (button 1) is generally used to press buttons, click menu items, select objects, and close boxes. The middle button (button 2) is used to paste data between clients or when held down, to scroll through scrollbars. The right button (button 3) is used for Properties menus or other information in the root display.

To demonstrate text copy and paste, first highlight text in one terminal window, then click the middle mouse button in another X terminal window. You can use this technique to copy URLs from a browser, paste commands into terminal windows, or move text between editing sessions.

# ## Changing the Pointer

The X pointer is the representation of your cursor when moving around the root window of your display or desktop. It generally changes to an “I” or text-editing cursor inside an active window. If you are a Mac OS user, you are probably familiar with a variety of pointers, such as the standard arrow and the animated watch.

Changing the root display pointer for your X session is fun and easy. The X pointers have names that correspond to definitions in the file `cursorfont.h`, found under the `/usr/X11R6/include/X11` directory. To change your pointer, use the `xsetroot` client with its `-cursor_name` option, followed by the name of a cursor like this:

```
```sh
# xsetroot -cursor_name gumbi
```
```

After you press Enter, your pointer will become an old and familiar friend. To reset your cursor, use the default pointer’s name like this:

```
```sh
# xsetroot -cursor_name X_cursor
```
```

Use the `xfd` client and its `-fn` option, followed by the name, which allows you to view available cursors, like this:

```
```sh
# xfd -fn cursor
```
```

After you press Enter, you will see the cursors in a dialog box, as shown in Figure 8.4.