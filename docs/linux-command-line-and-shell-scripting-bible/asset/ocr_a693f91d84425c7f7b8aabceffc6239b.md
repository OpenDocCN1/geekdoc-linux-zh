The first parameter defines a title for the menu. The next two parameters define the height and width of the menu window, while the third parameter defines the number of menu items that appear in the window at one time. If there are more menu items, you can scroll through them using the arrow keys.

Following those parameters, you must add menu item pairs. The first element is the tag used to select the menu. Each tag should unique for each menu item and can be selected by hitting the appropriate key on the keyboard. The second element is the text used in the menu. Figure 15-6 demonstrates the menu produced by the example command.

If a user selects a menu item by pressing the appropriate key for the tag, that menu item is highlighted but not selected. A selection isn't made until the OK button is selected, by using either the mouse or the Enter key. The dialog command sends the selected menu item text to STDERR, which you can redirect as needed.

# The fselect widget

There are several fancy built-in widgets provided by the dialog command. The fselect widget is extremely handy when working with filenames. Instead of forcing the user to type in a filename, you can use the fselect widget to browse to the file location and select the file, as shown in Figure 15-7.

FIGURE 15-6

The menu widget with menu items

![](bbox=[0.118, 0.553, 0.775, 0.903])