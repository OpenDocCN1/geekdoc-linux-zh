
## 8.9 Scrollbar

```tk
"moveto" {
# Get the fraction of the list to display as top
#
set topfract [lindex $cmdlist 1]

# And shift it for the appropriate
# size of the listboxes.

set topfract1 [expr $topfract * ($sizel/$size)]
set topfract2 [expr $topfract * ($size2/$size)]
}
```

```tk
# Move the listboxes to their new location
#
$listbox1 view moveto topfract1
$listbox2 view moveto topfract2

# Reposition the scrollbar slider
set topfract [expr ($topfract > $topfract2)? \
  $topfract1:$topfract2]
$scrollbar set $topfract \
  [expr $topfract + (($height-1)/$size)]
```

# Script Result

| Left Line 3 | Next Right 4 |
| :--- | :--- |
| Left Line 4 | Right Line 5 |
| Left Line 5 | Next Right 5 |
| Left Line 6 | Right Line 6 |
| Left Line 7 | Next Right 6 |

The calls to view in the previous example. The vview and xview subcommands set the start location for the data in a listbox. The first argument (scroll or moveto) is used to determine how to interpret the other arguments.

## Chapter 8. Introduction to Tk Graphics

When a scrollbar and a listbox are connected in the usual manner, with a line resembling

```
scrollbar .scroll -command ".box yview"
```

the scrollbar widget will append arguments describing how to modify the data to the arguments supplied in the -command argument and the new string will be evaluated. The arguments appended will start with either the word scroll or the word moveto.

For example, if an arrow were clicked in scrollbar .scroll, the command evaluated would be:

```
.box yview scroll 1 unit
```

The .box procedure would parse the first argument (yview) and evaluate the yview procedure. The yview code would parse the argument 1 unit to determine how the listbox should be modified to reflect scrolling 1 unit down.

In the previous example, the slider doesn't behave exactly as described for the default scrollbar procedures. Because we are scrolling lists of two different sizes, the slider size is set to reflect the fraction of data displayed from the larger listbox. The position of the slider reflects the center of the displayed data, rather than the start point. By changing the parameters to $control set you can modify that behavior. For instance, you could position the slider to reflect the condition of one listbox and treat the other listbox as a slave.

## 8.10 The scale Widget

The scale widget will allow a user to select a numeric value from within a given range. It creates a bar with a slider, similar to the scrollbar widget, but without arrows at the ends.

When the user moves the slider, the scale widget can either evaluate a procedure with the new slider location as an argument, or set a defined variable to the new value, or perform both actions.

## 8.10 The scale Widget

Syntax: `scale scaleName ?options?`

`scale` Create a scale widget.

`scaleName` The name for this scale widget.

`?options?` There are many options for this widget. The minimal set is:

- `-orient orientation` Whether the scale should be drawn horizontally or vertically: orientation may be horizontal or vertical. The default orientation is vertical.

- `-length numPixels` The size of this scale. The height for vertical widgets and the width for horizontal widgets. The height may be in any valid distance value (as described in Section 8.2.3).

- `-from number` One end of the range to display. This value will be displayed on the left side (for horizontal scale widgets) or top (for vertical scale widgets).

- `-to number` The other end for the range.

- `-label text` The label to display with this scale.

- `-command script` The command to evaluate when the state changes. The new value of the slider will be appended to this string, and the result string will be evaluated.

- `-variable varName` A variable that will contain the current value of the slider.

- `-resolution number` The resolution to use for the scale and slider. Defaults to 1.

- `-tickinterval number` resolution to use for the scale. This does not affect the values returned when the slider is moved.

The next example shows two scale widgets being used to display temperatures in Celsius and Fahrenheit scales. You can move either slider and the other slider will change to display the equivalent temperature in the other scale.

### Example 8.10-1

Example Script
```tk
# Convert the Celsius temperature to Fahrenheit
proc celsiusToFahren {ctemp} {
 global fahrenheit [expr ($ctemp*1.8) + 32]
}
```
```tk
# Convert the Fahrenheit temperature to Celsius
proc fahrToCelsius {ftemp} {
 global celsius
 set celsius [expr ($ftemp-32)/1.8]
}
```
```tk
# Create a scale for fahrenheit temperatures
set fahrescale [scale .fht -orient horizontal \
-from 0 to -100 -length 250 \
-resolution .1 -tickinterval 20 -label "Fahrenheit" \
-variable fahrenheit -command fahrToCelsius]
```
```tk
# Create a scale for celsius temperatures
scale .cel -orient horizontal \
-from 0 to -50 -length 250 \
-resolution .1 -tickinterval 10 -label "Celsius" \
-variable celsius -command celsiusToFahren]
```

## Chapter 8. Introduction to Tk Graphics

## 8.11 Windows

The `wm` command gives the Tk programmer access to the services provided by the window manager. These services vary slightly between window managers and operating systems. You should read the online documentation for the subcommands supported by wm.

By default, the window name is shown in the top decoration. This can be modified with the `wm` command.

### Example 8.11-1

Example Script
```tk
# Create the label.
label .1 -text "" -width 40
pack .1

# Assign some text.
set str "Tcl makes programming Fun"

# And add new text to the label one character at a time.
for {set i 0} $i < [string length $str]} {incr i} {
    tcl configure -text [string range $str 0 $i]
    update
    # Mark time for a second or so.
    #
    for {set j 0} $j < 1000} {incr j} {
        set x [expr $j.0*2]
    }
}
```

## 8.12 Interacting with the Event Loop

The Tk event loop is processed whenever the interpreter is not evaluating a command or procedure. It's best to write your code to spend as little time as possible within procedures. However, some tasks just take a while, and you may need to schedule passes through the event loop while your procedure is running.

You can force the Tcl interpreter to evaluate the event loop with the `update` command.

**Syntax:** `update ?idletasks?`

`update` Process the loop until all pending events have been processed.

`idletasks` Do not process user events or errors. Process only pending requests as updating the display.

A classic error in event-driven GUI programming is to perform some task in a loop, with a command to modify the display, and not force the display to update. In this case, only the last screen modification is displayed.

The next example shows a simple loop to put characters into a label. Without the update in the loop, the task would pause for several seconds and then display the complete string. The update command causes the characters to be displayed one at a time.

### Example 8.12-1

Example Script
```tk
#
# Create the label.
label .1 -text "" -width 40
pack .1

# Assign some text.
set str "Tcl makes programming Fun"

# And add new text to the label one character at a time.
for {set i 0} $i < [string length $str]} {incr i} {
    tcl configure -text [string range $str 0 $i]
    update
    # Mark time for a second or so.
    #
    for {set j 0} $j < 1000} {incr j} {
        set x [expr $j.0*2]
    }
}
```
