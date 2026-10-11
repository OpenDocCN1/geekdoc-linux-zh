# # Themes

You can think of a theme as a collection of styles. While each style is widget-specific (one for buttons, one for entries, etc.), a theme will collect many styles together. Typically, a theme will then define one style for each type of widget, but each of those styles will be designed so that they visually “fit” together with each other — though perhaps unfortunately Tk doesn’t technically restrict bad design or judgement!

To use a particular theme for an application is really to say that you’d like to have a set of styles defined so that by default all the different type of widgets will have some common appearance, and fit in well with each other.

# # Using Styles and Themes

So now we know what styles and themes are supposed to do, but how exactly do we use them? To do this, we need to know how to refer to styles and themes, and how to apply them to a widget or user interface.

# ## Style Names

Every style has a name. If you’re going to modify a style, create a new one, or use a style for a widget, you need to know its name.

How do you know what the names of the styles are? If you have a particular widget, and you want to know what style it is currently using, you can first check the value of its “style” configuration option. If that is empty, it means the widget is using the default style for the widget. You can retrieve that via the widget’s class. For example:

```
```
>>> b = ttk.Button()
>>> b['style']
''
>>> b.winfo_class()
'TButton'
```
```

So in this case, the style that is being used is “TButton”. The default styles for other themed widgets are named similarly, e.g. “TEntry”, “TLabel”, “TSizeGrip”, etc. It’s always wise to check specifics though; for example, the treewiew widget’s class is “Ttreeview”, not “TTtreeview”.

Beyond the default styles though, styles can be named pretty much anything. You might create your own style (or use a theme that has a style) named “FunButton”, “NuclearReactorButton”, or even “GuessWhatIAm” (not a smart choice). More often, you’ll find names like “Fun.TButton” or “NuclearReactor.TButton”, which suggest variations of a base style; as you’ll see, this is something Tk supports for creating and modifying styles.

> The ability to retrieve a list of all currently available styles is currently not supported.

# ## Using a Style

To use a style means to apply that style to an individual widget. If you know the name of the style you want to use, and which widget to apply it to, it’s easy. Setting the style can be done at creation time:

```
`b = ttk.Button(parent, text='Hello', style='Fun.TButton')`
```

As well, you can change the style of a widget at anytime after you’ve created it with the “style” configuration option:

```
`b['style'] = 'NuclearReactor.TButton'`
```

# ## Using Themes

While styles control the appearance of individual widgets, themes control the appearance of the entire user interface. The ability to switch between themes is one of the significant features of the themed widgets.