
## 9.4 More Canvas Widget Subcommands

The bounding box for all the items in the display can be used to define the scroll region.

### Example 9.4.6-1

Example Script

```t
canvas .c-row 0 -height 150 -scrollregion \
  [-100 -200 4500 2000] -yscrollcommand \
  ".scrollY X" -xscrollcommand ".scrollY X set" \
  -xscrollincrement 50 -yscrollincrement 25

scrollbar .scrollY -orient vertical -command ".c view"
scrollbar .scrollX -orient horizontal -command ".c view"

grid .c-row 0 -column 0
grid .scrollY-row -100 -column 1 -sticky ns
grid .scrollX-row 1 -column 0 -sticky ew

for {set y -200} {$y < 2000} {incr y 50} {
  set bottom [expr $y < 4500]
  for {set x -100} {$x < 500} {incr x 50} {
    set right [expr $x+50]

    if {{($y + $x) % 100} == 50} {
      set textColor white
      set fillColor black
    } else {
      set textColor black
      set fillColor white
    }
    .create rectangle $x $y right $bottom \
      -fill fillColor -outline gray30
    .create text [expr $x+25] [expr $y+25] \
      -text "$x\n$y" -font \
      [list helvetica 18 bold] -fill $textColor
  }
}
```

Chapter 9. The canvas Widget, Images, and Events

## Script Results

| 0 | 50 | 100 | 150 | -200 | -200 | -200 | 3550 | 3600 | 3650 | 3700 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 0 | 0 | 0 | 50 | 100 | 150 | 1450 | 1450 | 1450 | 1450 |
| 0 | 50 | 100 | 150 | -150 | -150 | -150 | 3550 | 3600 | 3650 | 3700 |
| 50 | 50 | 50 | 50 | 0 | 100 | 150 | 1500 | 1500 | 1500 | 1500 |
| 0 | 100 | 150 | 150 | -100 | -100 | -100 | 3550 | 3600 | 3650 | 3700 |
| 100 | 100 | 100 | 100 | 50 | 100 | 150 | 1550 | 1550 | 1550 | 1550 |

## 9.5 The bind and focus Commands

Section 9.1.3 mentioned that an event can be linked to a canvas item, and when that event occurs it can trigger an action. You can also bind actions to events on other widgets. This section will discuss how this is done.

Most of the Tcl widgets have some event bindings defined by default. For example, when you click on a button widget, the default action for the ButtonPress event is to evaluate the script defined in the -command option.

### 9.5.1 The bind Command

The bind command links an event to a widget and a script. If the event occurs while the focus is on that widget, the script associated with that event will be evaluated.

```
Syntax: bind widgetName eventType script
```

bind Define an action to be executed when an event associated with this widget occurs.

widgetName The widget to have an action bound to it.

eventType The event to trigger this action. Events can be defined in one of three formats:

alphanumeric A single printable (alphanumeric or punctuation) character defines a KeyPress event for that character.

300

```
<<virtualEvent>>
```

A virtual event defined by your script with the event command.

```
<modifier-type-detail>
```

This format precisely defines any event that can occur. The fields of an event descriptor are described below. Where two names are together, they are synonyms for each other. For example, either Button1 or B1 can be used to the left mouse button click.

modifier There may be one or more occurrences of the modifier field, which describes conditions that must exist when an event defined by the type field occurs. For example, Alt and Shift may be pressed at the same time as a letter KeyPress.

Not all computers support all the available modifiers. For instance, few computers have more than three buttons on the mouse, and most general-purpose computers don't support a Mod key.

The modifiers Double and Triple define double or triple mouse clicks.

Valid values for modifier are:

| Button1 | Button2 | Button3 | Button4 | Button5 |
| :--- | :--- | :--- | :--- | :--- |
| B1 | B2 | B3 | B4 | B5 |
| Mod1 | Mod2 | Mod3 | Mod4 | Mod5 |
| M1 | M2 | M3 | M4 | M5 |
| Meta | Alt | Control | Double | Triple |
| M | Lock | | | |

type This field describes the type of event. Only one type entry is allowed in an event descriptor.

Chapter 9. The canvas Widget, Images, and Events

Valid values for type are:

| KeyPress | Button | KeyRelease | ButtonRelease |
| :--- | :--- | :--- | :--- |
| Enter | Leave | FocusIn | FocusOut |
| Colormap | Configure | Deactivate | Destroy |
| Activate | Circulate | Gravity | Map |
| Motion | Property | Reparent | Unmap |
| Visibility | Expose | | |

The detail provides the final piece of data to identify an event precisely. The value that the detail field can take depends on the contents of the type field.

| type | detail |
| :--- | :--- |
| ButtonPress | detail will be the number of a mouse button (1–5). If the button number is specified, only events with that button will be bound to this action. |
| ButtonRelease | No detail is defined for a ButtonPress or ButtonRelease event, then any mouse-button event will be bound to this action. |
| KeyPress | detail will specify a particular key such as a 3 |
| KeyRelease | Nonalphanumeric keys are defined by names such as Space or Caps_Lock. An X11 Manual will list all of these, or you can run xkeycaps on a Unix/Linux system to get a list of the available types. |

No detail is defined for a KeyPress or KeyRelease event, then any keyboard event will be bound to this action.

## 9.5 The bind and focus Commands

### Bind Examples

| Event Definition | Description |
| :--- | :--- |
| <B1-Motion> | This event is generated if the left mouse button is pressed and the mouse moves, i.e., when you drag an item on a screen. |
| a | This event is generated if the left mouse button is pressed and the mouse moves, i.e., when you drag an item on a screen. |
| Shift_L | This event is generated if the left mouse button is pressed and the mouse moves, i.e., when you drag an item on a screen. |
| <Shift_L> | This event is generated if the left mouse button is pressed and the mouse moves, i.e., when you drag an item on a screen. |
| <KeyRelease-Shift_L> | This event is generated if the left mouse button is pressed and the mouse moves, i.e., when you drag an item on a screen. |
| <Control-Alt-Delete> | This event is generated if the left mouse button is pressed and the mouse moves, i.e., when you drag an item on a screen. |

The bind command can pass information about the event that occurred to the script that is be evaluated. This is done by including references to the events in the `script` argument. The complete list of the information available includes:

- %x The X component of the cursor's location when the event occurs.
- %y The Y component of the cursor's location when the event occurs.
- %b The button that was pressed or released if the event is ButtonPress or ButtonRelease.
- %k The key that was pressed or released if the event is KeyPress or KeyRelease.
- %A ASCII value of the key pressed or released if the event is KeyPress or KeyRelease.

&T The type of event that occurred.

&W The pathname of the window in which the event occurred.

## Bind Examples

- ...<KeyPress> {keystroke %k} Will invoke the procedure keystroke with the value of the key when a KeyPress event occurs.
- ...<Motion> {moveitem %x %y} Will invoke the procedure moveitem with the x and y location of the cursor when a Motion event occurs.

### 9.5.2 The Canvas bind Subcommand

Events can be bound to a drawable item in a canvas just as they are bound to widgets. The command to do this uses the same values for eventType and script as the bind command uses:

Syntax: canvasName bind tagOrId eventType script

The following example is a blueprint drawing with information attached to the items in the drawing, as was suggested in Section 9.1.1.1. Notice that both the canvasName bind command and the Tk widget bind command are used to bind actions to the events.

In the setInfo proc below, when a canvas item is double-clicked, it creates a label to display the information about that item. The cursor enters one of the labels on the right, the displayable items with tag are highlighted.

```cl

################################################
# proc setInfo {canv obj txt}--\-
# sets the 'information' associated with an item.
# binds displaying the information to a double-click event
# binds highlighting to <enter> and <leave> events.
# Arguments
# canv The canvas that contains this item
# obj The item identifier
# text Text to display when the item is double-click
```

304
