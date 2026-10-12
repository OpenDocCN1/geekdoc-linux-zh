These macro definitions, which appear at first glance to be harmless, will cause interesting things to happen during compilation of code for almost any graphic toolkit, not just Qt. Creating global variables, macros, and constant values causes trouble. Even if you assign unlikely names, there is a possibility that it will cause a conflict with someone else’s code later on.

A better way to address the need for “global” constants is to declare them within a class and simply inherit that class. This is the purpose served by the Qt class.

Many of the Qt widgets and classes accept constant flags, modifiers, and data values that are common across nearly all the widgets and many of the convenience classes. Rather than further pollute the name space, the Qt toolkit defines a class called Qt that exposes these common values to its subclassed objects. Since QObject—and many classes that are not based on QOоbject—inherit the Qt class, these enumerated constants are directly accessible from any class that is derived from one of these subclasses of Qt. Of course, there is nothing wrong with accessing one of these values explicitly; for example:

```
QColor r( Qt::red );
```

For any subclass of QObject or one of the other Qt subclasses, it is much easier to simply access the values as follows:

```
QColor r( red );
```

The classes QBrush, QCustomMenuItem, QEvent, QIconViewItem, QListViewItem, QObject, QPalette, QPen, QPixmap, QStyleSheet, QToolTip, and QWhatsThis all inherit the Qt class, so the constants are directly accessible by the methods of these subclasses and their subclasses in turn.

Table 6.1 lists the data type and constant name pairs.

Table 6.1 Data Type and Constant Name Pairs
| Value Type | Constant |
| :--- | :--- |
| ButtonState | NoButton, LeftButton, RightButton, MidButton, MouseButtonMask, ShiftButton, ControlButton, AltButton, KeyButtonMask |
| Orientation | Horizontal, Vertical |
| AlignementFlags | AlignLeft, AlignRight, AlignHCenter, AlignTop, AlignBottom, AlignVCenter, AlignCenter = AlignHCenter \| AlignVCenter, SingleLine, DontClip, ExpandTabs, ShowPrefix, WordBreak, DontPrint |
| WidgetState | WState_Created, WState_Disabled, WState_Visible, WState_ForcedHide, WState_OwnCursor, WState_MouseTracking, WState_CompressKeys, (continued) |