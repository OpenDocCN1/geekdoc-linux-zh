
## Part III: Advanced Shell Scripting

### FIGURE 18.5
The *textbox* widget.

![](img/0798d50a0e5dbf1265fbda3832b3e015_467_0.png)

You can use the arrow keys to scroll left and right, as well as up and down in the text file. The bottom line in the window shows the location percentage within the file that you're viewing. The *textbox* widget contains only a single Exit button, which you select to exit the widget.

## The *menu* widget

The *menu* widget allows you to create a window version of the text menu created earlier in this chapter. You simply provide a selection tag and the text for each item:

```bash
$ dialog --menu "Sys Admin Menu" 20 30 10 1 "Display disk space" \
  2 "Display users" 3 "Display memory usage" 4 "Exit" 2> test.txt
```

The first parameter defines a title for the menu. The next two parameters define the height and width of the menu window, and the third parameter defines the number of menu items that appear in the window at one time. If there are more menu items, you can scroll through them using the arrow keys.

Following those parameters, you must add menu item pairs. The first element is the tag used to select the menu item. Each tag should be unique for each menu item and can be selected by pressing the appropriate key on the keyboard. The second element is the text used in the menu. Figure 18.6 demonstrates the menu produced by the sample command.

If the user selects a menu item by pressing the appropriate key for the tag, that menu item is highlighted but not selected. A selection isn't made until the OK button is selected by using either the mouse or the Enter key. The `dialog` command sends the selected menu item text to STDERR, which you can redirect as needed.

## Chapter 18: Writing Scripts for Graphical Desktops

### FIGURE 18.6
The menu widget with menu items.

![](img/0798d50a0e5dbf1265fbda3832b3e015_468_0.png)

## The fselect widget

There are several fancy built-in widgets provided by the dialog command. The fselect widget is extremely handy when working with filenames. Instead of forcing the user to type a filename, you can allow them to use the fselect widget to browse to the file location and select the file, as shown in Figure 18.7.

### FIGURE 18.7
The fselect widget.

![](img/0798d50a0e5dbf1265fbda3832b3e015_468_1.png)

The `fselect` widget format looks like this:

```bash
$ dialog --title "Select a file" --fselect $HOME/ 10 50 2>file.txt
```

The first parameter after the `fselect` option is the starting folder location used in the window. The `fselect` widget window consists of a directory listing on the left side, a file listing on the right side that shows all the files in the selected directory, and a simple text box that contains the currently selected file or directory. You can manually type a filename in the text box, or you can use the directory and file listings to select one (use the spacebar to select a file to add to the text box).

## The dialog options

In addition to the standard widgets, you can customize lots of different options in the `dialog` command. You’ve already seen the `--title` parameter in action. This parameter allows you to set a title for the widget that appears at the top of the window.

Lots of other options allow you to completely customize both the appearance and the behavior of your windows. Table 18.2 shows the options available for the `dialog` command.

### TABLE 18.2 The dialog Command Options

| Option | Description |
| :--- | :--- |
| `--add-widget` | Proceeds to the next dialog unless the Esc key has been pressed or the Cancel button clicked |
| `--aspect-ratio` | Specifies the width/height aspect ratio of the window |
| `--backtitle title` | Specifies a title to display on the background, at the top of the screen |
| `--begin x y` | Specifies the starting location of the top-left corner of the window |
| `--cancel-label label` | Specifies an alternative label for the Cancel button |
| `--clear` | Clears the display using the default dialog background color |
| `--colors` | Embeds ANSI color codes in dialog text |
| `--cr-wrap` | Allows newline characters in dialog text and forces a line wrap |
| `--create-rc file` | Dumps a sample configuration file to the specified file |
| `--defaultno` | Makes the default of a yes/no dialog No |
| `--default-item string` | Sets the default item in a checklist, form, or menu dialog |
| `--exit-label label` | Specifies an alternative label for the Exit button |
| `--extra-button` | Displays an extra button between the OK and Cancel buttons |
| `--extra-label label` | Specifies an alternative label for the Extra button |
| `--help` | Displays the `dialog` command help message |
| `--help-button` | Displays a Help button after the OK and Cancel buttons |
| `--help-label label` | Specifies an alternative label for the Help button |
| `--help-status` | Writes the checklist, radiolist, or form information after the help information if the Help button was clicked |
| `--ignore` | Ignores options that dialog does not recognize |
| `--input-fd fd` | Specifies a file descriptor other than STDIN |
| `--insecure` | Changes the password widget to display asterisks when typing |
| `--item-help` | Adds a help column at the bottom of the screen for each tag in a checklist, radiolist, or menu for the tag item |
| `--keep-window` | Doesn’t clear old widgets from the screen |
| `--max-input size` | Specifies a maximum string size for the input; the default is 2048 |
| `--nocancel` | Suppresses the Cancel button |
| `--no-collapse` | Doesn’t convert tabs to spaces in dialog text |
| `--no-kill` | Places the tailboxbg dialog in the background and disables SIGHUP for the process |
| `--no-label label` | Specifies an alternative label for the No button |
| `--no-shadow` | Doesn’t display shadows for dialog windows |
| `--ok-label label` | Specifies an alternative label for the OK button |
| `--output-fd fd` | Specifies an output file descriptor other than STDERR |
| `--print-maxsize` | Prints the maximum size of dialog windows allowed to the output |
| `--print-size` | Prints the size of each dialog window to the output |
| `--print-version` | Prints the dialog version to output |
| `--separate-output` | Outputs the result of a checklist widget one line at a time with no quoting |
| `--separator string` | Specifies a string that separates the output for each widget |
| `--separate-widget string` | Specifies a string that separates the output for each widget |
| `--shadow` | Draws a shadow to the right and bottom of each window |
| `--single-quoted` | Uses single quoting if needed for the checklist output |
| `--sleep sec` | Delays for the specified number of seconds after processing the dialog window |
| `--stderr` | Sends output to STDERR—the default behavior |
| `--stdout` | Sends output to STDOUT |
| `--tab-correct` | Converts tabs to spaces |
| `--tab-len n` | Specifies the number of spaces a tab character uses; the default is 8 |
| `--timeout sec` | Specifies the number of seconds before exiting with an error code if no user input |
| `--title title` | Specifies the title of the dialog window |
| `--trim` | Removes leading spaces and newline characters from dialog text |
| `--visit-items` | Modifies the tab stops in the dialog window to include the list of items |
| `--yes-label label` | Specifies an alternative label for the Yes button |

The `--backtitle` option is a handy way to create a common title for your menu through the script. If you specify it for each dialog window, it persists throughout your application, creating a professional look for your script.

As you can tell from Table 18.2, you can overwrite any of the button labels in your dialog window. This feature allows you to create just about any window situation you need.

### Using the dialog command in a script

Using the dialog command in your scripts is a snap. Just remember two things:

- Check the exit status of the dialog command if a Cancel or No button is available.
- Redirect STDERR to retrieve the output value.

If you follow these two rules, you'll have a professional-looking interactive script in no time. Here's an example using dialog widgets to reproduce the system admin menu created earlier in the chapter:

```bash
$ cat menu3
#!/bin/bash
# using dialog to create a menu

temp=$(mktemp -t test.XXXXXX)
temp2=$(mktemp -t test2.XXXXXX)

function dipkspace {
df -k > $temp
dialog --textbox $temp 20 60
}

function whoseon {
who > $temp
dialog --textbox $temp 20 50
}
```
