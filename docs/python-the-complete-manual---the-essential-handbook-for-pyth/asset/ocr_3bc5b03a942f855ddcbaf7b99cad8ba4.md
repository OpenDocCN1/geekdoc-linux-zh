# # Build tic-tac-toe with Kivy Create with Python

entry point for the creation of our GUI. We can start
making the simplest Kivy app possible:

```
from kivy.app import App

class TicTacToeApp(App):
    pass

if __name__ == "__main__":
    TicTacToeApp().run()
```

You can easily run this, your app will start up and
you'll get a plain black window. Exciting!
We can build our own GUI out of Kivy widgets.
Each is a simple graphics element with
specific behaviour of its own ranging from
standard GUI functionality (eg the Button, Label
or TextInput), to those positioning on
child widgets (eg the BoxLayout, Floating
or GridLayout), to abstracting a more
involved task like interacting with hardware (eg
TheFileChooser, Camera or VideoPlayer). Importantly, Kivy's widgets are designed to be easily
combined - than including including widget for every
need imaginable, widgets are kept simple but
easy to join new interfaces. We'll see some
of that in this tutorial.

![](bbox=[0.535, 0.114, 0.945, 0.383])

```
def build(self):
    return Label(text='Hello World!',
                 font_size=100,
                 color=(r, g, b, a))
```

The 'build' method is called when the 'App' is,
and whatever is returned automatically
the root of App. In our case
that's a Label, and we've set several properties - the
'text', 'font_size' and 'color'. All widgets have different
properties controlling aspects of their behaviour
which can be dynamically updated to their
appearance, here we see them just once\upon instantiation.

Since 'Hello World' is compulsory in any
programming tutorial, let's get it over by using a
simple 'Label' widget to display the:

+   - Note that properties are not just Python
attributes but inside Kivy properties. These are
accessed like normal attributes but provide extra
functionality by hooking into Kivy's event system.
- We'll see examples of creating properties, and
you should do the same if you want to use your
variables with Kivy's event and binding functionality.
- All you need to show some simple text, so
run the program again to check that this works.
You experiment with the parameters if it's unclear
what any of them are.

from kivy.ui.label import Label

We'll display the 'Label' by returning it as our app'soot widget. Every app has a single root widget,
top level of its text, and it will automatically be
sized to fill the window. We'll see later how to
construct a GUI by adding more widgets for this
one, but for now it's enough to set the root widget
by adding a new method to the 'App':