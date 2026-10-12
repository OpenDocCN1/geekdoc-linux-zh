hard-coded x, y coordinates and width, height sizing. It's not easy (sometimes it's impossible) to accurately represent an abstract layout scheme that can be dramatically affected by each widget's runtime properties such as font size or contents.

A good understanding of, and a lot of experience with, the QLayout based classes will allow you to quickly implement complex forms with only a preliminary sketch of what the form should look like. It takes practice, but a programmer with that skill can implement a complex dialog using relative layout just about as quickly as a programmer who uses a WYSIWYG dialog editor can generate a less elegant, hard-coded interface that doesn't resize nearly as well. Most Motif programmers already know this quite well.

**QHBox, QVBox, and QGrid** These classes manage the geometry of widgets in rows, columns, or both, and display each managed widget in a separate frame. These classes are of little practical use---with the possible exception being state/status indicators on a status bar, as frequently seen in many Microsoft Windows applications. However, they can be used to provide simple management in “quickie” applications that don't have strict layout requirements.

**QLayoutItem, QWidgetItem, and QSpacerItem** QLayoutItems are the abstract items on which QLayout operates. QWidgetItems are QLayoutItems specific to QWidgets. A QSpacerItem is simply an empty QLayoutItem you can use for spacing purposes.

**QLayout** The base class for all layouts, QLayout provides an abstraction of the functions that are common to QBoxLayouts and QGridLayouts.

The online reference documentation provides an example of a custom layout based on QLayout. If you have a need for special layouts that can't be easily implemented using combinations of the provided layout classes, this is the obvious place to begin.

**QBoxLayout, QHBoxLayout, and QVBoxLayout** QBoxLayout manages widgets in either a horizontal or vertical direction. QHBoxLayout and QVBoxLayout are convenience implementations that provide horizontal or vertical layouts, respectively.

# A Possible Instantiation

```
```cpp
// Create a top-level layout with a spacing of ten pels
QBoxLayout *top = new QBoxLayout(this, 10);
```
```

# Example Use

```
```cpp
QBoxLayout *top = new QBoxLayout(this, 10);
QHBoxLayout *hb = new QHBoxLayout();
```
```