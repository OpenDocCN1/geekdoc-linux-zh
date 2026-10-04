Typing this code at the % prompt will display "Hello, world" in a small box in the graphics window:

```
label .1 -text "Hello, world"
pack .1
```

The label command tells the wish interpreter to construct a graphics widget named .1 and place the text "Hello, world" within that widget.

The pack command causes the label to be displayed. This will be covered in Chapter 8.

When you run this little script you should see a window resembling this on your screen:

![](bbox=[0.483, 0.396, 0.598, 0.442])

# 2.3 Evaluating Tcl Script Files

Typing a short program at the command line is a good start, but it doesn't create a shipp product. The next step is to evaluate a Tcl script stored in a file on disk.

# 2.3.1 The Tcl Script File

A Tcl script file is simply ASCII text file of Tcl commands. The individual commands may be terminated with a newline marker (carriage return or linefeed) or a semicolon. If a command is too long to fit on a single line, making the last character before the newline a backslash will continue the same command line on the next screen line.

For example, here's a simple tsh script that prints several lines of information.