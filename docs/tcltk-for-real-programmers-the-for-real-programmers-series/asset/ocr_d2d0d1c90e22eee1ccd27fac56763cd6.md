# 8.7 Widget Layout: frame, place, pack, and grid

options? The options for a frame include:

+   -height numPixels
Height in pixels.

+   -width numPixels
Width in pixels.

+   -background color
The color of the background.

+   -relief ?sunken?raised?
Defines how to draw the border edges—can make the frame look raised or sunken.
The default is not to display relief borders.

+   -borderwidth width
Sets the width of the decorative borders.
The width value may be any valid size value (as described in Section 8.2.3).

A display can be divided into frames by functionality; for example, an application that interfaces with a database would have an area for the user to enter query fields, an area with the database displays, an area of buttons to generate searches, etc. This could be broken down into three primary frames: .entry-Frame, .displayFrame, and .buttonFrame. Within each of these frames would be the other widgets, with names such as .entryFrame.userName, .display-Frame.securityRating, and .buttonFrame.search.

# 8.7.2 The Place Command

The place command lets you declare precisely where a widget should appear in the display window. This location can be declared as an absolute location or a relative location based on the size of the window. Applications that use few widgets or need precise control are easily programmed with the place layout manager. For most applications, however, the place manager has too much programmer overhead.

Syntax: place widgetName option ?options?

place Declare the location of a widget in the display.