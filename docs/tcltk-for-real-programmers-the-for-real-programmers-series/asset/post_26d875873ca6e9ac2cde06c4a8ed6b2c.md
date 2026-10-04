
# Chapter 8. Introduction to Tk Graphics

## 8.13 Scheduling the Future: after

The previous example uses a busy loop to cause the script to pause between inserting characters into the label. This is a pretty silly waste of CPU time and Tcl provides a better way to handle this.

The after command will perform one of two tasks:

- *If called with a single numeric argument, it will pause for that many milliseconds.
- If called with a numeric argument and a script, it will schedule that script to be run the requested number of milliseconds in the future and continue processing the current script.

**Syntax:** after milliseconds ?script?

| argument | description |
| :--- | :--- |
| after | Pause processing of the current script, or schedule a script to be processed in the future |
| milliseconds | The number of milliseconds to pause the current processing, or the number of seconds in the future to evaluate another script |
| script | If this argument is defined, this script will be evaluated after milliseconds time has elapsed |

The next example shows the after command being used instead of the busy loop. Then it shows events being scheduled in the future to remove the characters from the label.

### Example 8.13-1

### Example Script

```tcl
#
# Create the label.
label .1 -text "" -width 40
pack .1

# Assign some text.
set str "Tcl makes programming Fun"

# And add new text to the label one character at a time. 
```

```tcl
for {set i 1} {$i < [string length $str]} {incr i} {
  .l configure -text [string range $str 0 $i]
  update
  after 1000
}
############################################################
# proc shortenText {widget}
# Remove the first character from the displayed string of a
# widget
# Arguments
# widget      The name of a widget with a -text option
#
# Results
# Removes the first character from the text string of the
# provided widget if one exists.
#
# Schedules itself to run again if the -text string wasn't
# empty.
proc shortenText {widget} {
  # Get the current text string from the widget
  #
  set txt [$widget cget -text]
  # If it's empty, we're done.
  #
  if {$txt == ""} {
    return;
  }
  # shorten the string
  #
  set txt [string range $txt 1 end]
  # Update the widget
  #
  $widget configure -text $txt
  # And schedule this procedure to be run again in 1 second.
  #
  after 1000 shortenText $widget
}
shortenText .1
```

The first loop (filling the widget) is the type of process that occurs immediately by programmers who are used to working in non-event-driven paradigms.

The style of programming demonstrated by the shortenText procedure of using the after command is less intuitive but more versatile.

In the first style, the event loop is checked only once per second. If there were an ABORT button, there would be a noticeable lag between a button click and the task being aborted. Using the second style, the GUI will respond immediately.

### 8.13.1 Canceling the Future

Sometimes, after you've carefully scheduled things, plans change and schedules need to change.

When the after command is evaluated, it returns a handle for the event that was scheduled in the future. This handle can be used to manipulate the list of scripts scheduled for evaluation. In particular, you can use this handle to cancel an event:

Syntax: after cancel handle

```tcl
after cancel
Cancel a script that was scheduled to be evaluated in the future.
```

```tcl
handle The handle for this event that was returned by a previous after script command.
```

We'll use the after cancel command in the next chapter.

## 8.14 Bottom Line

This chapter has introduced most of the Tk primitive widgets. The mega-widgets (fileboxes, color selectors, etc.), the text widget, and the canvas widget will be covered in the next three chapters.

The Tk primitive widgets provide the tools necessary to write GUI-oriented programs with support for buttons, entry widgets, graphics display widgets, scrolling listboxes, menus, and numeric input.

Tk widgets can be arranged on the display using the place, grid, or pack layout manager.

The update command can be used to force a pass through the event loop during long computations.

The after command can be used to pause an application or to schedule a script for evaluation in the future.

The after cancel command can be used to cancel a script that was scheduled to be evaluated in the future.

# Chapter 9. The canvas Widget, Images, and Events

Chapter 8 described many of the Tk widgets that support GUI programming. This chapter will discuss the canvas widget, Tcl events, and the Tk image object. It will show how events can be connected to a drawable item on a canvas or an entire widget and how to use a canvas to build your own GUI widgets.

The canvas is the Tk widget drawing surface. You can draw lines, arrows, rectangles, ovals, text, or random polygons in various colors with various fill styles. You can also insert images in X-Bitmap, PPM (Portable PixMap), PGM (Portable GrayMap), or GIF (Graphical Interface Format) format (other formats are supported in various Tk extensions, which will be discussed in Chapter 13). If that's not enough, you can write C code to add new types to the canvas command.

As mentioned in Chapter 8, Tk is event oriented. Whenever a cursor moves or a key is pressed, an event is generated by the windowing system. If the focus for your window manager is on a Tk window, event is passed to the Tk interpreter, which can then trigger actions connected with graphic items in that window.

The *bind* command links scripts to the events that occur on graphic items such as widgets or displayed items in a canvas or text widget. Events include mouse motion, button clicks, key presses, and window manager events such as refresh, iconify, or resize.

After we've discussed the *canvas* and *bind* command, I'll show you how to use them to create a toolbar widget similar to the ones in MS-Windows and Netscape.

## 9.1 Overview of the canvas Widget

Your application may create one or more canvas widgets and map them to the display with any of the layout managers *pack, grid,* or *place*. The canvas owns all items that are drawn on it. These items are maintained in a display list and their position in that list determines which items will be drawn on top of others. The order in which items are displayed can be modified.

### 9.1.1 Identifiers and Tags

When an item is created on a canvas, a unique numeric identifier is returned for that item. The item can always be identified and manipulated by referencing that unique number.

You can also attach a tag to an item. A tag is an alphanumeric string that can be used to group canvas items. A single tag can be attached to multiple items, and multiple tags can be attached to a single item.

A set of items that share a tag can be identified as a group by that tag. For example, if you composed a blueprint of a house, you could tag all of the plumbing with plumbing and then tag the hot water pipes with hot, the cold water pipes with cold, and the drains with drain. You could highlight all of the plumbing with a command like:

```bash
$blueprint configure plumbing -outline red
```

Two tags are defined by default in a canvas widget:
- all Identifies all the drawable items in a canvas.
- current Identifies the topmost item selected by the cursor.

### 9.1.2 Coordinates

The canvas coordinate origin is the upper left-hand corner. Larger Y coordinates move down the screen, and larger x coordinates move to the right. The coordinates can be declared in pixels, inches, millimeters, centimeters, or points (1/72 of an inch), as described for dimensions in 8.2.3.

The coordinates are stored internally using floating-point format, which allows a great deal of flexibility for scaling and positioning. Note that even pixel locations can be fractional.

### 9.1.3 Binding

You can cause a particular script to be evaluated when an event associated with a displayed item occurs. For instance, when the cursor passes over a button, an ENTER event is generated by the window manager. The default action for the enter event is to change the button color to denote the button as active. Some widgets, such as the button widget, allow you to set the action for a button click event during widget creation with the -command option. All widgets can have actions linked to events with the bind command, which we will discuss in detail later in this chapter.

The canvas widget takes the concept of binding further and allows you to bind an action to events that occur on each drawable item within the canvas display list. For instance, you can make lines change color when the cursor passes over them or bind a procedure to a button click on item.

You can bind actions to displayed items either by tag (to cause an action to occur whenever an item tagged as plumbing is clicked, for instance) or by ID (to cause an action when a particular graphic item is accessed).
