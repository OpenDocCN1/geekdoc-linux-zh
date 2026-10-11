
A gauge is a thermometer bar showing the percentage progress. New percentages are read one at a time from standard input until the end of file is reached. The `~gauge` switch requires a text message, the height, width, and an optional starting percentage (see Listing 13.2). The percentages can be sent to the gauge by a named pipe, discussed in Chapter 11, "Text File Basics."

Suppose you would like to show a thermometer graph showing the progress of printing a series of invoice files stored in a directory called `invoices`. The following demo displays the invoices as they are sent another script called `print_invoice`.

## Listing 13.2 `gauge_demo.sh`

```bash
#!/bin/bash
#
# gauge_demo.sh: a thermometer graph demo

shopt -s -o nounset

declare -rx SCRIPT=$0
declare -rx QUEUE=/status_fifo
declare -rx INVOICES_DIR="invoices"
declare -ix TOTAL_INVOICES=0
declare -ix NUM_INVOICES=0
declare -ix PERCENT=0

# count the invoices waiting to print
TOTAL_INVOICES=$(ls -1 $INVOICES_DIR | wc -l)

# create the pipe
mkfifo $QUEUE
if [ $? -ne 0 ] ; then
    printf "%s\n" "$SCRIPT:$LINENO: unable to create $QUEUE" >&2
    exit 192
fi

# print the invoices in a background subshell
# print the progress to the pipe
(
    cd $INVOICES_DIR
    ls -1 | (
        while read INVOICE ; do
            let "NUM_INVOICES++"
            print_invoice "$INVOICE"
            PERCENT=100*$NUM_INVOICES/$TOTAL_INVOICES
            printf "%d\n" "$PERCENT"
        done
    )
) > $QUEUE &

# display the progress.  dialog will stop when nothing
# more is printed by the subshell
dialog --gauges "Printing invoices" 7 70 0 < $QUEUE

wait          # wait for the subshell to finish
rm $QUEUE     # delete the pipe
sleep 1       # make sure results can be read by user

exit 0
```

An *info box* is a status message to the user. It has no buttons and the `dialog` command completes immediately. The `--infobox` switch requires a text message, as well as a height and width.

```bash
$ dialog --infobox "Connecting to server" 7 70
```

An *input box* enables the user to type a response. The `--inputbox` switch requires the prompt text, the height, width, and an optional default response for the user.

```bash
$ dialog --print-size --inputbox "Connect to which host?" 7 70 0  2> size.txt
$ cat size.txt
Size: 7, 70
$ rm size.txt
$ dialog --print-size --no-shadow --nocancel --inputbox \
    "Connect to which host?" 7 70
```

The remaining dialog boxes are similar to the ones already discussed.

-   A *menu* is a list of selections that the user can make a choice from. The `--menu` switch requires the menu heading text, the height, width, and the menu height. Each item is specified with a tag name and the menu item’s text.
-   A *message box* presents a message to the user with a single **OK** button. The `--msgbox` switch requires the text message, as well as the height and width.
-   A *password box* is similar to an input box except what the user types is not shown. The `--passwordbox` requires the text message, the height and width, and an optional default password.
-   A *radio list* presents a list of choices of which the user can select only one item. The `--radiolist` switch requires the heading text, the height, width, and the list height. Each item is specified the same way as a checklist.
-   A *tail box* displays final text in a file as if the `tail -f` command were used. The `--tailbox` switch requires the filename, as well as the height and width.
-   A *text box* shows the contents of a text file in the dialog box. The user can browse through the file. The `--textbox` switch requires the filename, height, and width.
-   The *background text box* is a combination of a tail box and a text box. The text is viewed as if the “tail -f” command was used, but the user is free to browse the content. The `--textboxbg` switch requires a filename, the height, and width.
-   A *time box* enables the users to select a time. The `--timebox` switch requires prompt text, a height, a width, and the initial time in hours, minutes, and seconds.
-   A *calendar box*, shown in Figure 13.3, shows a calendar and enables the users to select a date. The `--calendar` switch requires prompt text, a height, a width, and the day, month, and year to start with.

![](img/7da864b222941ec315ee1c456ff472dd_264_0.png)

Figure 13.3 A Calendar dialog box.

You can combine consecutive dialog boxes with the `--and-widget` switch.

```bash
$ dialog -inputbox "Connect to which host?" 7 70 "" -and-widget -inputbox \
"And what TCP/IP port?" 7 70
```

You must give an input box an initial string parameter (as `""` for none) or *dialog* assumes that `-and-widget` is the optional string.

There are a large number of switches for customizing the appearance and behavior of the boxes. These are listed in the reference section of this chapter.

## Reference Section

### showkey Command Switches

-   -scancodes (or -s)—Scancode dump mode
-   -keycodes (or -k)—Keycode dump mode (default)
-   -ascii (or -a)—ASCII dump mode

### setleds Command Switches

-   -caps—Clears Caps Lock
-   +caps—Sets Caps Lock
-   -D—Changes both console flags and LEDs
-   -F—Changes the console flags (default)
-   -L—Changes the LEDs
-   -num—Clears Num Lock
-   +num—Sets Num Lock
-   -scroll—Clears Scroll Lock
-   +scroll—Sets Scroll Lock

### dumpkeys Command Switches

-   -charset=c (or -c C)—Interprets character code values according to character set c
-   -compose-only—Shows only compose key combinations
-   -full-table (or -f)—Shows key bindings in canonical form
-   -funcs-only—Shows function key string definitions
-   -keys-only—Shows key bindings without string definitions
-   -long-info (or -1)—Prints detailed info about the keyboard driver
-   -numeric (or -n)—Shows values in hexadecimal format
-   -short-info (or -i)—Prints summary info about the keyboard driver

### setterm Command Switches

-   -append [ c ]—Dumps a console screen (default is current) to a file, appending it if the file exists
-   -appcursorkeys [on|off]—Sets Cursor Key Application Mode on or off
-   -background c—Sets the background text color to color c
-   -blank [ 0-60 ]—Number of minutes until the screen is blanked (default is 0, which is no blanking)
-   -blength [ n ]—Console beep duration in milliseconds (default is 0)
-   -bfreq h—Console beep frequency (pitch) in Hertz (default is 0)
-   -blink [on|off]—Turns blinking text printing on or off. When not on a console, turning blinking text off also turns off all other attributes
-   -bold [on|off]—Turns bold printing on or off. When not on a console, turning bold off also turns off all other attributes
-   -clear [ all|rest ]—Clears the screen and homes the cursor. rest clears to end of screen
-   -clrtabs [ tab1 tab2 tab2 ... ]—Clears Tab stops
-   -cursor [on|off]—Turns the console cursor on or off
-   -defaultc—Restores rendering options to their default values
-   -dump [ c ]—Saves a console screen (default is current) to a file
-   -file f—Sets the -dump or -append filename
-   -foreground c—Sets the foreground text color to color c
-   -half-bright [on|off]—Turns dim printing on or off. When not on a console, turning dim off also turns off all other attributes
-   -hcolor c—Sets the color for half-bright characters
-   -initialize—Restores the drawing characteristics to their default values
-   -inversescreen [on|off]—Inverts the screen colors
-   -linewrap [on|off]—Turns automatic line-wrapping on or off
-   -msg [on|off]—Enables or disables printk kernel messages
-   -msglevel n—Sets the printk message level to n
-   -reset—Restores the screen to its power-on state
-   -reverse [on|off]—Turns reverse color text printing on or off. When not on a console, turning reverse color text off also turns off all other attributes
-   -softscroll [on|off]—Turns soft keyboard scrolling on or off
-   -store—Saves the current rendering options as the defaults
-   -tabs [tab1 tab2 tab3 . . . ]—Sets the Tab stop positions
-   -term terminal_name—Uses terminal_name instead of value of the TERM variable
-   -ulcolor c—Sets the color for underlined characters
-   -underline [on|off]—Turns underline printing on or off. ulcolor is used if underlining is not supported

### dialog Command Switches

-   -aspect r—Line width ratio r based on the length of the prompt string to use as a guide to forcibly wrap lines that are too long relative to the dialog box (default is 9)
-   -backtitle b—A string b to be displayed on the backdrop, at the top of the screen
-   -beep—Beeps each time the screen is redrawn
-   -beep-after—Beeps if input is interrupted
-   -begin y x—The position of the upper-left corner of a dialog box, as opposed to centering
-   -clear—Clears the screen on exit
