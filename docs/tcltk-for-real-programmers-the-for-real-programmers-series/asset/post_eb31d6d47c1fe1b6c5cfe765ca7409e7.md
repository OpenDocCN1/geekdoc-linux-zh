
## 8.7 Widget Layout: frame, place, pack, and grid

options? The options for a frame include:

- -height numPixels
Height in pixels.

- -width numPixels
Width in pixels.

- -background color
The color of the background.

- -relief ?sunken|raised?
Defines how to draw the border edges—can make the frame look raised or sunken.
The default is not to display relief borders.

- -borderwidth width
Sets the width of the decorative borders.
The width value may be any valid size value (as described in Section 8.2.3).

A display can be divided into frames by functionality; for example, an application that interfaces with a database would have an area for the user to enter query fields, an area with the database displays, an area of buttons to generate searches, etc. This could be broken down into three primary frames: .entryFrame, .displayFrame, and .buttonFrame. Within each of these frames would be the other widgets, with names such as .entryFrame.userName, .displayFrame.securityRating, and .buttonFrame.search.

### 8.7.2 The Place Command

The place command lets you declare precisely where a widget should appear in the display window. This location can be declared as an absolute location or a relative location based on the size of the window. Applications that use few widgets or need precise control are easily programmed with the place layout manager. For most applications, however, the place manager has too much programmer overhead.

Syntax: place widgetName option ?options?

place Declare the location of a widget in the display.

widgetName The name of the widget being placed.

option The place command requires at least one of these placement options:

- An absolute location in pixels
- x xLocation
- y yLocation
- A relative location given as a fraction of the window
- relx xLocation
- rely yLocation
- The parent window for this widget. The parent may be a frame or top-level window, such as ".".

The following example uses the place command to build a simple application that calculates 15% sales tax on purchases. As you can see, there is a lot of overhead in placing widgets. You need a good idea of how large widgets will be, how large your window is, etc. in order to make a pretty screen.

# Example 8.7.2-1

```
# Create the "quit" and "calculate" buttons
set quitbutton [button .quit -text "Quit" -command exit]
set gobutton [button .gobutton -text "Calculate" -command {set salesTax [expr $userInput * 0.15]}]
```

```
# Create the label prompt and entry widgets
set input [entry .input -textvariable userInput]
set prompt [label .prompt -text "Base Price:"]
```

```
# Create the label and result widgets
set tax [label .tax -text "Tax: "]
set result [label .result -textvariable salesTax -relief raised]
```

# 8.7 Widget Layout: frame, place, pack, and grid

# Set the size of the window
.configure -width 250 -height 100

# Place the buttons near the bottom
place $quitbutton -relx .7 -rely .7
place $gobutton -relx .0 -rely .7

# Place the input widgets near the top.
place $prompt -x 0 -y 0
place $input -x 70 -y 0

# Place the results widgets in the middle
place $tax -x 0 -y 30
place $result -x 40 -y 30

# Script Result
![](img/fdcc2919568b5c9f5301d50a0247_0.png)

### 8.7.3 The pack Command

The pack command is quite a bit easier than place. With the pack command, you declare the positions of widgets relative to each other and let the pack command worry about the details.

Syntax: pack widgetName *options*

- pack Place and display the widget in the display window.
- widgetName The widget to be displayed.
- options The pack has many options. These options are the most used:
- side Declares that this widget should be packed closest to a given side of the parent window. The side argument may be one of top, bottom, left, or right. The default is top.
- expand boolean If set to 1 or yes, the widget will be expanded to fill available space in the parent window. The default is 0: do not expand to fill the space. The boolean argument may be one of 1, yes, or no.
- fill direction Defines whether a widget may expand to fill extra space in its parcel. The direction argument may be:
- none Do not fill
- x Fill horizontally
- y Fill vertically
- both Fill both horizontally and vertically
The default is none.
- padx number Declares how many pixels to leave as a gap between widgets.
- pady number Declares how many pixels to leave as a gap between widgets.
- after widgetName Pack this widget after (on top of) widgetName.

The pack algorithm works by allocating a rectangular parcel of display space and filling it in a given direction. If a widget does not require all the available space in a given dimension, the parent widget will “show through” unless the -expand or -fill option is used.

The following example shows how a label widget will be packed with a frame with various combinations of the -fill and -expand options being used.

# Example 8.7.3-1

```
Example Script

# Create a root frame with a black background, and pack it.
frame .root -background black
pack .root

# Create a frame with two labels to allocate 2 labels worth
# vertical space.
# Note that the twoLabels frame shows through where the top
# label doesn't fill.

frame .root.twoLabels -background gray50
label .root.twoLabels.upperLabel -text "twoLabels no fill top"
label .root.twoLabels.lowerLabel -text "twoLabels no fill lower"

pack .root.twoLabels -side left
pack .root.twoLabels.upperLabel -side top
pack .root.twoLabels.lowerLabel -side bottom

# Create a frame with no fill or expand options used.
# Note that the .nofill frame is completely covered by the
# label, and the root frame shows at the top and bottom

frame .root.nofill -background gray50
label .root.nofill.label -text "nofill, noexpand"

pack .root.nofill -side left
pack .root.nofill.label

# Create a frame and label pair with the -fill option used when
# the frame is packed.
# In this case, the frame fills in the Y dimension to use all
# available space, and the label is packed at the top of
# the frame. Thefill frame shows through below.

frame .root.fill_frame -background gray50
label .root.fill_frame.label -text "fill frame"

pack .root.fill_frame -side left -fill y
pack .root.fill_frame.label

# In this case, the frame is set to the size required to hold
# the widget, and the widget uses all that space.
frame .root.fill_label -background gray50
label .root.fill_label.label -text "fill label"
pack .root.fill_label -side left
pack .root.fill_label.label -fill y

# Allow both the frame and widget to fill the.
# The frame will fill the available space,
# but the label will not expand to fill the frame.
frame .root.fillBoth -background gray50
label .root.fillBoth.label -text "fill label and frame"
pack .root.fillBoth -side left -fill y
pack .root.fillBoth.label -fill y

# Allow both the frame and widget to expand and fill.
# The -expand option allows the widget to expand into
# space.
# The -fill option allows the widget to fill the available
# space.
frame .root.expandFill -background gray50
label .root.expandFill.label -text "expand and fill label and frame"
pack .root.expandFill -side left -fill y -expand y
pack .root.expandFill.label -fill y -expand y
```
