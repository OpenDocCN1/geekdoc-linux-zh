```
Button.label -sticky nsw

```
}
}
```
```

This starts to make sense; we have four elements, named "Button.border", "Button.focus", "Button.spacing", and "Button.label". Each of these has different element options, such as "-children", "-sticky", and "-border" that here specify layout or sizes. Without getting into too much detail at this point, we can clearly see the nested layout, based on the "-children" and "-sticky" attributes; Tk uses a simplified version of Tk's "pack" geometry manager to specify element layout.

# Element Options

Each of these different elements may have a number of different options. For example, the thumb of the scrollbar may have an option to set its background color, or another to provide the width of a border, if any. These can be customized to adjust how the elements within the widget look.

What options are available for each element? Here’s an example of checking what options are available for the label inside the button (which we know from the "layout" command is identified as "Button.label"):

```
```python
>>> s.element_options('Button.label')
('-compound', '-space', '-text', '-font', '-foreground', '-underline', '-width', '-anchor', '-justify', '-wraplength', '-embossed', '-image', '-stipple', '-background')
```
```

Presumably these options shouldn't have the leading dash on them.

In the next sections, we'll take a look at the not-entirely-straightforward way that you can work with element options.

# Changing Style Options

In this section, we'll look at how you can change the style’s appearance via modifying style options. You can do this either by modifying an existing style, or more typically, by creating a new style.

# Modifying a Style Option

Modifying a configuration option for an existing style is done in a similar fashion as modifying any other configuration option, by specifying the style, name of the option, and new value:

```
```python
s.configure('TButton', font=helvetica 24)
```
```

You'll learn more about what the valid options are shortly.

If you need to retrieve the current value of an option, this can be done with the "lookup" method.

```
```python
>>> s.lookup('TButton', 'font')
'helvetica 24'
```
```

# Creating a New, Derived Style

If you modify an existing style, such as "TButton", that modification will apply to all widgets using that style (so by default, all buttons). That may well be what you want to do.

More often, you're interested in creating a new style that is similar to an existing one, but varies in a certain aspect. For example, you'd like to have most of the buttons in your application keep their normal appearance, but create certain special "emergency" buttons, which will be highlighted in a different way. In this case, creating a new style (e.g. "Emergence.TButton") derived from the base style ("TButton") would be the appropriate thing to do.