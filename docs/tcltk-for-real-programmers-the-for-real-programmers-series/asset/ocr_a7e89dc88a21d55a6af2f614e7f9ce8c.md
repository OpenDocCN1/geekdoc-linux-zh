# Chapter 8. Introduction to Tk Graphics

The -sticky option lets your script declare that a widget should “stick” to the north (top), south (bottom), east (right), or west (left) edge of the grid that it’s placed within. By default, a widget is centered within its cell.

Any of the options for the grid command can be reset after a widget is packed with the grid configure command.

```
Syntax: grid configure widgetName -option optionValue
grid configure
```

Change one or more of the configuration options for a widget previously positioned with the grid command.

widgetName The name of the widget to have a configuration changed.

-option -optionValue
The option and value to modify (or set).

# Example 8.7.4-1

```
Example Script
set quitbutton [button .quitbutton -text "Quit" -command "exit"]
set gobutton [button .gobutton -text "Calculate Sales Tax" \-command {set salesTax [expr userInput * 0.15]}]}
setset input [entry .input -textvariable userInput]
set prompt [label .prompt -text "Base Price:"]
set tax [label .tax -text "Tax:"]
set result [label .result -textvariable salesTax -relief raised]
grid $quitbutton $gobutton -row 3
grid $prompt input -row 1
grid $tax $result -row 2 -sticky w
```