
# Making Time

For our final exercise, we will make something useful; a large character clock. To do this, we first need to install a program called banner. The banner program accepts one or more words as arguments and displays them like so:

```bash
me@linuxbox~$ banner "BIG TEXT"

###### ###### ###### ######
#      #  #      #  #      #  #      #
#      #  #      #  #      #  #      #
#      #  #      #  #      #  #      #
#      #  #      #  #      #  #      #
###### ###### ###### ######
```

This program has been around for a long time and there are several different implementations. On Debian-based systems (such as Ubuntu) the package is called "sys--banner", on Red Hat-based systems the package is called simply "banner". Once we have banner we can run this script to display our clock:

```bash
#!/bin/bash

# clock - Display a clock in a terminal

FG_BLUE=$(tput setaf 4)
FG_BLACK=$(tput setaf 0)
FG_WHITE=$(tput setaf 7)

terminal_size() { # Calculate the size of the terminal
    terminal_cols=$(tput cols)
    terminal_rows=$(tput lines)
}

banner_size() {
    # Because there are different versions of banner, we need to
    # calculate the size of our banner's output

    banner_cols=0
    banner_rows=0

    while read; do
        [[ $(($REPLY) -gt $banner_cols ]] && banner_cols=$($REPLY)
        ((+banner_rows))
    done <(banner "12:34 PM")
}

display_clock() {
    # Since we are putting the clock in the center of the terminal,
    # we need to read each line of banner's output and place it in the
    # right spot.

    local row=$clock_row

    while read; do
        tput cup $row $clock_col
        echo -n "$REPLY"
        ((+row))
    done <(banner "$(date +%I:%M %p)")
}

# Set a trap to restore terminal on Ctrl-c (exit).
# Reset attributes, make cursor visible, and restore
# previous screen contents (if possible).

trap 'tput cnorm; tput rmcup || clear; exit 0' SIGINT

# Save screen contents and make cursor invisible
tput smcup;; tput civis

# Calculate sizes and positions
terminal_size=
banner_size=
clock_row=$((terminal_rows - banner_rows) / 2))
clock_col=$((terminal_cols - banner_cols) / 2))
progress_row=$((clock_row + banner_rows) + 1))
progress_col=$((terminal_cols - 60) / 2))

# In case the terminal cannot paint the screen with a background
# color (tmux has this problem), create a screen-size string of
# spaces so we can paint the screen the hard way.

blank_screen=
for ((i=0; i < (terminal_cols * terminal_rows); ++i)); do
    blank_screen+=" "
done

# Set the foreground and background colors and go!
echo -n ${FG_BLUE}${FG_WHITE}
while true; do
    # Set the background and draw the clock
    if tput bce; then
        # Paint the screen the easy way if bce is supported
        clear
    else
        # Do it the hard way
        tput home
        echo -n "$blank_screen"
    fi

    tput cup $clock_row $clock_col
    display_clock

    # Draw a black progress bar then fill it in white
    tput cup $progress_row $progress_col
    echo -n "${FG_BLACK}"
    echo -n "##################################################"
    tput cup $progress_row $progress_col
    echo -n "${FG_WHITE}"

    # Advance the progress bar every second until a minute is used up
    for ((i = $(date +%s);i < 60; ++i)); do
        echo "#"
        sleep 1
    done
done
```

![](img/9aafc495f4afbc0a97de2b31a0d13f46_83_0.png)
