Note that you can enter either a geometry or an offset, but you can't enter
only XOFF or width by itself. Both the geometry and the offset have to be
entered as a pair. That is, you can't enter

```
> xterm -geometry 80
```

or

```
> xterm -geometry +0
```

but the following will work:

```
> xterm -geometry 80x25
```

or

```
> xterm -geometry +0+0
```

There's one other way to specify default settings for X programs, and this is
through the .Xdefaults file. Anything you can set through the command line
be stored in the .Xdefaults file when you start the program, you don't
need to give all the options. These options are known as resources.

# 16.6 X RESOURCES

An X resource can consist of four item types:

program.widget[..].resource: value

where:

program: Program name
widget: One or more levels of widgets, which are sub-portions of the win-
dow. A widget can be a button, menu, scrollbar, option list, and so on.
resource: The "least common denominator" of the widgets. The resource
be used by more than one program. For example "geometry" is
used by all X programs and is a resource.
value: What the resource gets set to. Can be a number, boolean (true or
alse), color, or some other value. It depends on the resource.

Any text from a ! to the end of the line is commented out.