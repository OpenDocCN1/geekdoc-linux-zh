```
# Set the background and draw the clock
\if tput bce; then $ Paint the screen the easy way if bce is supported
clear
else $ Do it the hard way
tput home
echo -n "$blank_screen"
fi

tput cup $clock_row $clock_col
display_clock
```

```
# Draw a black progress bar then fill it in white
tput cup $progress_row $progress_col
echo -n "${PG_BLACK}"
echo -n "##################################################"
tput cup $progress_row $progress_col
echo -n "${PG_WHITE}"
```

```
# Advance the progress bar every second until a minute is used up
for ((i = $(date +%s);i < 60; ++i)); do
echo "#"
sleep 1
done
```

![](bbox=[0.176, 0.438, 0.822, 0.707])

| # # # # ###### | # # |
| # # # # # # # # # # # # |
| # # # # # # # # # # # # |
| # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # |

# clock script in action

Our script paints the screen blue and places the current time in the center of the terminal window. This script does not dynamically update the display's position if the terminal is resized(that's an enhancement left to the reader). A progress bar is displayed beneath the clock and it is updated every second until the next minute is reached, when the clock itself is updated.

One interesting feature of the script is how it deals with painting the screen. Terminals that support the “bce” capability erase the current background color. So, on

14 tput