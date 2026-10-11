By prepending another name ("Emergency") followed by a dot onto an existing style, you are implicitly creating a new style derived from the existing one. So in this example, our new style will have exactly the same options as a regular button except for the indicated differences:

```
```
s.configure('Emergency.TButton', font=helvetica 24, foreground='red', padding=10)```
```

# ## State Specific Style Options

Besides the normal configuration options for the style, the widget author may have specified different options to use when the widget is in a particular widget state. For example, when a button is disabled, you'd like to have the color of the button's label greyed out.

To do this, you can specify a "map", which allows you to specify variations for one or more of a style's configuration options. For each configuration option, you can specify a list of widget states, along with the particular value the option should be assigned when the widget is in that state.

> Remember that the state is composed of one or more state flags (or their negation), as set by the widget's "state" method, or queried via the "instase" method.

The following example provides for the following variations from a button's "normal" appearance:

+   - when the widget is in the disabled state, the background color should be set to "#d9d9d9"  
+   - when the widget is in the active state (mouse over it), the background color should be set to "#feecec"  
+   - when the widget is in the disabled state, the foreground color should be set to "#3a3a3a" (this is in addition to the background color change we already noted)  
+   - when the widget is in the state where the button is pressed and the widget is not disabled, the relief should be set to "sunken"  
+   PYTHONTODO

Remember that in the past, with classic Tk widgets, exactly what changed when the widget was in each state would have been determined solely by the widget author. With themed widgets, it is the style itself that determines what changes, which could include things that the original widget author had never anticipated.

> Because widget states can contain multiple flags, it's possible that more than one state will match for an option (e.g. "pressed" and "pressed !disabled" will both match if the widget's "pressed" state flag is set). The list of states is evaluated in the order you provide in the map command, with the first state in the list that matches being used.

# ## Sound Difficult to you?

So you now know that styles are made up of elements, which have a variety of options, and are composed together in a particular layout. You can change various options on styles, to make all widgets using the style appear differently. Any widgets using that style take on the appearance that the style defines. Themes collect an entire set of related styles, making it easy to change the appearance of your entire user interface.

So what makes styles and themes so difficult in practice? Three things. First:

You can only modify options for a style, not element options (except sometimes).

We talked earlier about how to discover what elements were used in the style by examining the style's layout, and also how to discover what options were available for each element. But when we went to make changes to a style, we seemed to be configuring an option for the style, without specifying an individual element. What's going on?

84