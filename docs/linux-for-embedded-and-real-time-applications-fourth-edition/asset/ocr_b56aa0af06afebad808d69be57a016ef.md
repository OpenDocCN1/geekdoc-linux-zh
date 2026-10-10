![](bbox=[0.35, 0.07, 0.85, 0.41])

**Figure 11.1**
Signals and slots.

# *A Simple Example*

To get a feel for how QT works, let us start with a simple example of a text edit window.
The source code is shown in *Listing 11.1*. Each QT class has its own header file with the
same name as the class. The header `QtGui` in line 2 pulls in all of the GUI class headers.

Line 6 creates a `QApplication` object. This object manages application-wide resources, and is
necessary to run any QT program that has a GUI. It needs `argv` and `args`, because QT accepts
a few command line arguments. Line 8 creates a text edit widget, and line 9 creates a push
button widget with the text “Quit.” Then, in line 11 we connect the `clicked()` signal of the
`quitButton` to the `quit()` slot of the application. The `quit()` function terminates the program.

Line 13 creates a Vertical Box Layout widget. Widgets can contain other widgets. In this
case, lines 14 and 15 make `textEdit` and `quitButton` children of `layout`. The layout widget
organizes its children in a window, in this case vertically. Line 18 puts `layout` in a
window, and line 20 displays the window. Finally, line 22 causes the `QApplication` to enter
its event loop. QT applications are event-driven. Events are generated and sent to the
application’s widgets. Examples of events are mouse presses and key strokes. When you
type text in the text edit widget, it receives key pressed events, and responds by drawing
the text typed.