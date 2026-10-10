
## Options Table

| Option | Description |
| :--- | :--- |
| `--extra-button` | Displays an extra button between the OK and Cancel buttons |
| `--extra-label label` | Specifies an alternative label for the Extra button |
| `--help` | Displays the dialog command help message |
| `--help-button` | Displays a Help button after the OK and Cancel buttons |
| `--help-label label` | Specifies an alternative label for the Help button |
| `--help-status` | Writes the checklist, radiolist, or form information after the help information if the Help button was clicked |
| `--ignore` | Ignores options that dialog does not recognize |
| `--input-fd fd` | Specifies a file descriptor other than `STDIN` |
| `--insecure` | Changes the password widget to display asterisks when typing |
| `--item-help` | Adds a help column at the bottom of the screen for each tag in a checklist, radiolist, or menu for the tag item |
| `--keep-window` | Doesn’t clear old widgets from the screen |
| `--max-input size` | Specifies a maximum string size for the input; default is 2048 |
| `--nocancel` | Suppresses the Cancel button |
| `--no-collapse` | Doesn’t convert tabs to spaces in dialog text |
| `--no-kill` | Places the tailboxbg dialog in background and disables `SIGHUP` for the process |
| `--no-label label` | Specifies an alternative label for the No button |
| `--no-shadow` | Doesn’t display shadows for dialog windows |
| `--ok-label label` | Specifies an alternative label for the OK button |
| `--output-fd fd` | Specifies an output file descriptor other than `STDERR` |
| `--print-maxsize` | Prints the maximum size of dialog windows allowed to the output |
| `--print-size` | Prints the size of each dialog window to the output |
| `--print-version` | Prints the dialog version to output |
| `--separate-output` | Outputs the result of a checkList widget one line at a time with no quoting |
| `--separator string` | Specifies a string that separates the output for each widget |
| `--separate-widget string` | Specifies a string that separates the output for each widget |
| `--shadow` | Draws a shadow to the right and bottom of each window |
| `--single-quoted` | Uses single quoting if needed for the checklist output |
| `--sleep sec` | Delays for the specified number of seconds after processing the dialog window |
| `--stderr` | Sends output to `STDERR` - the default behavior |
| `--stdout` | Sends output to `STDOUT` |
| `--tab-correct` | Converts tabs to spaces |
| `--tab-len n` | Specifies the number of spaces a tab character uses; default is 8 |
| `--timeout sec` | Specifies the number of seconds before exiting with an error code if no user input |
| `--title title` | Specifies the title of the dialog window |
| `--trim` | Removes leading spaces and newline characters from dialog text |
| `--visit-items` | Modifies the tab stops in the dialog window to include the list of items |
| `--yes-label label` | Specifies an alternative label for the Yes button |

Lots of other options allow you to completely customize both the appearance and the behavior of your windows. Table 18.2 shows the options available for the dialog command.

The `--backtitle` option is a handy way to create a common title for your menu through the script. If you specify it for each dialog window, it persists throughout your application, creating a professional look for your script.

As you can tell from Table 18.2, you can overwrite any of the button labels in your dialog window. This feature allows you to create just about any window situation you need.

### Using the dialog command in a script

Using the dialog command in your scripts is a snap. Just remember two things:

- Check the exit status of the dialog command if a Cancel or No button is available.
- Redirect `STDERR` to retrieve the output value.

If you follow these two rules, you'll have a professional-looking interactive script in no time. Here's an example using dialog widgets to reproduce the system admin menu created earlier in the chapter:

```bash
$ cat menu3
#!/bin/bash
# using dialog to create a menu

temp=$(mktemp -t test.XXXXX)
temp2=$(mktemp -t test2.XXXXX)

function diskspace {
    df -k > $temp
    dialog --textbox $temp 20 60
}

function whoseon {
    who > $temp
    dialog --textbox $temp 20 50
}

function memusage {
    cat /proc/meminfo > $temp
    dialog --textbox $temp 20 50
}

while [ 1 ]
do
    dialog --menu "Sys Admin Menu" 20 30 10 1 "Display disk space" 2 \
    "Display users" 3 "Display memory usage" 0 "Exit" 2> $temp2
    if [ $? -eq 1 ]
    then
        break
    fi

    selection=$(cat $temp2)

    case $selection in
    1) diskspace ;;
    2) whoseon ;;
    3) memusage ;;
    0) break ;;
    *) dialog --msgbox "Sorry, invalid selection" 10 30
    esac
done
rm -f $temp 2> /dev/null
rm -f $temp2 2> /dev/null
$
```

The script uses the `while` loop with a constant true value to create an endless loop displaying the menu dialog. This means that, after every function, the script returns to displaying the menu.

The menu dialog includes a Cancel button, so the script checks the exit status of the `dialog` command in case the user presses the Cancel button to exit. Because it's in a `while` loop, exiting is as easy as using the `break` command to jump out of the while loop.

The script uses the `mktemp` command to create two temporary files for holding data for the dialog commands. The first one, `$temp`, is used to hold the output of the `df`, `who`, and `meminfo` commands so that they can be displayed in the textbox dialog (see Figure 18-8). The second temporary file, `$temp2`, is used to hold the selection value from the main menu dialog.

Now this is starting to look like a real application that you can show off to people!

## Getting Graphic

If you're looking for even more graphics for your interactive scripts, you can go one step further. Both the KDE and GNOME desktop environments (see Chapter 1, “Starting with Linux Shells”) have expanded on the dialog command idea and include commands that produce X Windows graphical widgets for their respective environments.

This section describes the kdialog and zenity packages, which provide graphical window widgets for the KDE and GNOME desktops, respectively.

![](img/a5025f22e05b92f409563a958cac7312_669_0.png)

**FIGURE 18-8** The meminfo command output displayed using the textbox dialog option

## The KDE environment

The KDE graphical environment includes the kdialog package by default. The kdialog package uses the kdialog command to generate standard windows, similar to the dialog-style widgets, within your KDE desktop. However, instead of having the clunky feel to them, these windows blend right in with the rest of your KDE application windows. This allows you to produce Windows-quality user interfaces directly from your shell scripts.

> **NOTE**
>
> Just because your Linux distribution uses the KDE desktop doesn't necessarily mean it has the kdialog package installed by default. You may need to manually install it from the distribution repository.

### kdialog widgets

Just like the dialog command, the kdialog command uses command-line options to specify what type of window widget to use. Here is the format of the kdialog command:

```bash
kdialog display-options window-options arguments
```

The `display-options` allow you to customize the window widget, such as add a title or change the colors. The `window-options` are what allow you to specify what type of window widget to use. The available options are shown in Table 18.3.

### TABLE 18.3 kdialog Window Options

| Option | Description |
| :--- | :--- |
| `--checklist title [tag item status]` | A checklist menu, with status specifying whether or not the item is checked |
| `--error text` | Error message box |
| `--inputbox text [init]` | Input text box where you can specify the default value using the init value |
| `--menu title [tag item]` | Menu selection box title and a list of items identified by a tag |
| `--msgbox text` | Simple message box with specified text |
| `--password text` | Password input text box that hides user input |
| `--radiolist title [tag item status]` | A radiolist menu, with status specifying whether or not the item is selected |
| `--separate-output` | Returns items on separate lines for checklist and radiolist menus |
| `--sorry text` | Sorry message box |
| `--textbox file [width] [height]` | Text box displaying the contents of file, alternatively specified by width and height |
| `--title title` | Specifies a title for the TitleBar area of the |
