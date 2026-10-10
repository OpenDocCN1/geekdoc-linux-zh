
## Using kdialog

You can use the `kdialog` window widgets in your shell scripts similarly to how you use the `dialog` widgets. The big difference is that the `kdialog` window widgets output values using `STDOUT` instead of `STDERR`. Here's a script that converts the system admin menu created earlier into a KDE application:

```bash
$ cat menu4
#!/bin/bash
# using kdialog to create a menu

temp=$(mktemp -t temp.XXXXXX)
temp2=$(mktemp -t temp2.XXXXXX)

function diskspace {
  df -k> $temp
  kdialog --textbox $temp 1000 10
}

function whoseon {
  who> $temp
  kdialog --textbox $temp 500 10
}

function memusage {
  cat /proc/meminfo> $temp
  kdialog --textbox $temp 300 500
}

while [ 1 ]
do
kdialog --menu "Sys Admin Menu" "1" "Display disk space" "2" "Display users" "3" "Display memory usage" "0" "Exit"> $temp2
if [ $? -eq 1 ]
then
  break
fi

selection=$(cat $temp2)

case $selection in
1)
  diskspace ;;
2)
  whoseon ;;
3) memusage ;;
0) break ;;
*)
    kdialog --msgbox "Sorry, invalid selection"
esac
done
$
```

The script using the `kdialog` command isn't much different from the one using the `dialog` command. The resulting main menu is shown in Figure 18-10.

![](img/a5025f22e05b92f409563a958cac7312_675_0.png)

**FIGURE 18-10** The sys admin menu script using kdialog

Now your simple shell script looks just like a real KDE application! There's no limit to what you can do with your interactive scripts now.

## The GNOME environment

The GNOME graphical environment supports two popular packages that can generate standard windows:

- gdialog
- zenity

By far, `zenity` is the most commonly available package found in most GNOME desktop Linux distributions (it’s installed by default in both Ubuntu and CentOS). This section describes the features of `zenity` and demonstrates how to use it in your shell scripts.

### zenity Widgets

As you would expect, `zenity` allows you to create different window widgets by using command-line options. **Table 18.4** shows the various widgets that `zenity` can produce.

**TABLE 18.4** The zenity Window Widgets

| Option | Description |
| :--- | :--- |
| `--calendar` | Displays a full month calendar |
| `--entry` | Displays a text entry dialog window |
| `--error` | Displays an error message dialog window |
| `--file-selection` | Displays a full pathname and filename dialog window |
| `--info` | Displays an informational dialog window |
| `--list` | Displays a checklist or radiolist dialog window |
| `--notification` | Displays a notification icon |
| `--progress` | Displays a progress bar dialog window |
| `--question` | Displays a yes/no question dialog window |
| `--scale` | Displays a scale dialog window with a sliding bar to select the value within a range |
| `--text-info` | Displays a text box containing text |
| `--warning` | Displays a warning dialog window |

The `zenity` command-line program works somewhat differently than the `kdialog` and `dialog` programs. Many of the widget types are defined using additional options on the command line, instead of including them as arguments to an option.

The `zenity` command does offer some pretty cool advanced dialog windows. The `--calendar` option produces a full month calendar, as shown in **Figure 18-11**.

![](img/a5025f22e05b92f409563a958cac7312_677_0.png)

**FIGURE 18-11** The zenity calendar dialog window

When you select a date from the calendar, the `zenity` command returns the value to `STDOUT`, just like `kdialog`:

```bash
$ zenity --calendar
12/25/2011
$
```

![](img/a5025f22e05b92f409563a958cac7312_678_0.png)

**FIGURE 18-12** The zenity file selection dialog window

Another pretty cool window in `zenity` is the file selection option, shown in Figure 18-12.

You can use the dialog window to browse to any directory location on the system (as long as you have the privileges to view the directory) and select a file. When you select a file, the `zenity` command returns the full file and pathname:

```bash
$ zenity --file-selection
/home/ubuntu/menu5
$
```

With tools like that at your disposal, the sky's the limit with your shell script creations!

### Using zenity in scripts

As you would expect, `zenity` performs well in shell scripts. Unfortunately, the creators of `zenity` chose not to follow the option convention used in `dialog` and `kdialog`, so converting any existing interactive scripts to `zenity` may prove challenging.

In converting the system admin menu from `kdialog` to `zenity`, we had to do quite a bit of manipulation of the widget definitions:

```bash
$ cat menu5
#!/bin/bash
# using zenity to create a menu

temp=$(mktemp -t temp.XXXXXX)
temp2=$(mktemp -t temp2.XXXXXX)

function diskpace {
  df -k> $temp
  zenity --text-info --title "Disk space" --filename=$temp \
  --width 750 --height 10
}

function whoseon {
  who> $temp
  zenity --text-info --title "Logged in users" \
  --filename=$temp \
  --width 500 --height 10
}

function memusage {
  cat /proc/meminfo> $temp
  zenity --text-info --title "Memory usage" \
  --filename=$temp \
  --width 300 --height 500
}

while [ 1 ]
do
  zenity --list --radiolist --title "Sys Admin Menu" --column "Select" \
  --column "Menu Item" FALSE "Display disk space" \
  FALSE "Display users" \
  FALSE "Display memory usage" FALSE "Exit"> $temp2
  if [ $? -eq 1 ]
  then
     break
  fi

selection=$(cat $temp2)
case $selection in
"Display disk space")
  diskpace ;;
"Display users")
  whoseon ;;
"Display memory usage")
  memusage ;;
Exit)
  break ;;
*)
  zenity --info "Sorry, invalid selection"
esac
done
$
```

Because `zenity` doesn't support the menu dialog window, we used a `radiolist` type window for the main menu, as shown in Figure 18-13.

![](img/a5025f22e05b92f409563a958cac7312_680_0.png)

**FIGURE 18-13** The system admin menu using zenity

The radiolist uses two columns, each with a column heading. The first column includes the radio buttons, and the second column is the item text. The radiolist also doesn't use tags for the items. When you select an item, the full text of the item is returned to `STDOUT`. This makes life a little more interesting if you use the `case` command. You must use the full text from the items in the case options. If there are any spaces in the text, you need to use quotation marks around the text. Using the `zenity` package, you can add a Windows feel to your interactive shell scripts in the GNOME desktop.

## Working Through a Practical Example

The one downside to each of these graphical packages is that there isn't a way to create a window with multiple entries, such as combining several text box inputs along with a calendar input, as you can do in a true graphical environment. That limitation does make querying for multiple data items a bit clunky, but it's still manageable. The trick is to keep track of each data query using appropriately named variables.

The `dialog` package does include a form feature, but it's fairly elementary. It only allows you to combine several text boxes into a single window to enter multiple data items. The format for the `--form` option is:

```bash
--form text height width formheight [ label y x item y x flen ilen ] ...
```

The parameters used by the `--form` option are as follows:

- **text**: A title that appears at the top of the form
- **height**: The total form window height
- **width**: The total form window width
- **formheight**: The total height of the form within the window
- **label**: The label for the form field
- **y**: The Y position of the label or item within the form
- **x**: The X position of the label or item within the form
- **item**: A default value to assign to a form field
- **flen**: The length of the form field to display
- **ilen**: The maximum length of the data that can be entered into
