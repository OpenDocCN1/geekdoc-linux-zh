
The second argument to the `if` command is a Tcl script, which can contain any number of Tcl commands. This script is executed if the expression contained in the first argument evaluates to True.

The `if` commands can have one or more `elseif` commands and one `else` command associated with them. The syntax for these commands is shown here:

```
if {expr} {
    commands
}
elif {expr} {
    commands
}
elif {expr} {
    commands
}
else {
    commands
}
```

The commands associated with the first `if` or `elseif` whose expression evaluates to True are executed. If none of these expressions evaluate to True, the commands associated with the `else` command are executed.

> **WARNING**
The open brace must occur on the same line as the word that precedes it. This is because new lines are treated as command separators. If you enter an `if` command where the `if {expr}` portion of the command appears on one line and the rest is on the next line, it is treated as two separate commands.

## The for Command

The `for` command in Tcl provides a way of implementing for loops. Tcl for loops are very similar to for loops in other languages, such as C. The `for` command expects four arguments. The first argument is a script that is used to initialize the counter. The second argument is an expression that is evaluated each time through the loop to determine whether to continue. The third argument is used to define the increment to be used on the counter. The fourth argument is the set of commands to be executed each time through the loop.

```
for { set i 0} {$i < 10} {incr I 1} {
    puts [expr 2 * $i]
}
```

The preceding loop executes ten times. The counter `i` is initially set to 0. The `for` loop executes while `i` is less than 10, and the value of `i` is increased by 1 each time through the loop. The command that is executed each time through the loop is the puts command. This evaluates 2 * i each time through the loop and prints the result to the screen. The output that results from running this command is listed here:

0
2
4
6
8
10
12
14
16
18

## The while Command

The while command is used to implement while loops in Tcl. while loops are very similar to for loops. The only real difference between them is that the for loop provides more enhanced features for controlling entrance and exit criteria for the loop. The syntax for the while loop is shown in the following example:

```
set I 0
while {$i < 10} {
    puts [expr 2 * $i]
    set i [expr $i + 1]
}
```

This while loop performs the same function as the example that was presented in the section describing the for loop. It calculates 2 * i each time through the loop and prints the result to the screen. Notice that in this example you have to handle incrementing the counter yourself. With the for loop, the counter incrementing was taken care of by the for command.

## The switch Command

The switch command provides the same function as an if statement that has multiple elseif clauses associated with it. The switch command compares a value (this value is usually stored in a variable) with any number of patterns, and if it finds a match it executes the Tcl code associated with the matching pattern.

```
switch $thing {
    car {puts "thing is a car"}
    truck {puts "thing is a truck"}
    default {puts "I don't know what this thing is"}
}
```

The `Tcl switch` command is equivalent to the `case` statement found in Pascal and some other languages. This `switch` command compares the value that is stored in the `thing` variable (which must be set prior to these statements, of course) with the string `car` and the string `truck` to see if it matches either of them. If the value of the `thing` variable is equal to `car`, then `thing is a car` is displayed on the screen. If the value of the `thing` variable is equal to `truck`, then `thing is a truck` is displayed on the screen. If neither of these cases is true, the `default` clause is executed and `I don't know what this thing is` displays on the screen.

> **TIP**
Whenever you need to check to see if a variable is equal to one of a number of values, use a `switch` command instead of an `if` command with multiple `elseif` clauses. This makes the code much easier to read and understand.

## Comments

It is always a good idea to include comments in any Tcl code you write—or code you write in any other language, for that matter. This becomes especially important if any of the following situations are possible:

- Someone else needs to look at or maintain your code.
- Your programs get large.
- You won't be looking at code that you have written for long periods of time after you write it.

Chances are that at least one of these situations will come up with Tcl code you have written.

Comments cannot be placed in the middle of a command. They must occur between commands. The pound sign (#) is used to inform Tcl to expect a comment.

```
# This is a valid comment

set a 1 ;  # This is a valid comment

set a 1    # This is an invalid comment
```

The third comment shown here is invalid because it occurs in the middle of a command. Remember that Tcl interprets everything up to a newline character or a semicolon to be part of the command.

## The Tk Language Extensions

Earlier in this chapter, a simple example of Tk displayed HELLO there in a button in the wish window. Tk is much more powerful than that example showed. Along with the button widget are many other widgets provided by Tk. These include menus, scrollbars, and list boxes. This section gives you an overview of some of the other Tk widgets, as well as short examples explaining how these widgets can be used.

## Frames

Frame widgets are containers for other widgets. They do not have any interesting behavior like the other Tk widgets. The only visible properties of frame widgets that you can set are the color and border appearance. You can give three different border appearances to a frame widget: flat, raised, and sunken. You can experiment with the different frame widgets to see how they look.

The flat border frame widget is not especially interesting. It looks exactly the same as the default wish window (because the default border appearance is flat).

## Buttons

Button widgets are used to get specific input from a user. A button can be turned on or activated by the user of a Tk program by moving the mouse pointer over the button and then pressing the left mouse button. Tk provides the following three kinds of button widgets:

- Button
- Check button
- Radio button

The button widget is used to initiate some specific actions. The button usually has a name such as “Load file” that describes the action that results if you press the button.

Check button widgets are used to allow users of a program to turn program options on or off. When the check button is shaded the program option is on, and when the check button is not shaded the program option is off.

Radio buttons are similar to check buttons except that they are defined in groups, where only one member of a group of radio buttons is allowed to be on at one time. This means that if one radio button in a group of radio buttons is on, none of the other radio buttons in that group can be turned on. When the radio button is shaded it is on, and when the radio button is not shaded it is off.

## Menus and Menu buttons

Menu widgets are used to implement pull-down menus, cascading menus, and pop-up menus. A menu is a top-level widget that contains a set of menu entries that have values or commands associated with them. Five kinds of entries can be used in menus:

- Cascade entries display a submenu when the mouse pointer passes over them. The cascade entry is similar in function to the menu button widget.
- Command entries invoke a Tcl script when activated. The command entry is similar to the button widget in function.
- Check button entries toggle a program option between on and off. When the check button is shaded the option is on, and when the check button is not shaded it is off. The check button entry is similar in function to the check button widget.
- Radio button entries toggle a program option. The difference between the radio button entry and the check button entry is that radio buttons are typically defined in groups, with the restriction that only one of the radio buttons in the group can be active at once. The radio button entry is similar in function to the radio button widget.
- Separator entries display a horizontal line in the menu. This is used for appearance purposes only. There is no behavior associated with a separator entry.

The main difference between the menu entries and the button widgets is that the button widgets can exist by themselves, but the menu entries must exist within the context of a menu widget.

Menu button widgets are similar to button widgets. The only real difference between the two is that when menu buttons are invoked they bring up menus instead of executing Tcl scripts as button widgets do. The menu button name usually describes the types of menu entries contained in the menu that the menu button activates. This means that you will find menu entries that perform some kind of file operations contained within the File menu.

You can activate a menu by moving the mouse pointer to the menu button widget and pressing the left mouse button. This activates the menu associated with the menu button and displays the menu entries that are contained in that menu to the screen. You can now move the mouse pointer down through the list of menu entries and select the one you want.

The File menu contains two command entries (the Open entry and Quit entry), one cascade entry (the Save As entry), and one separator entry. The menu that comes up as a result of clicking the mouse pointer on the Save As cascade entry contains three command entries: the Text entry, the Ver 1 file entry, and the Ver 2 file entry.
