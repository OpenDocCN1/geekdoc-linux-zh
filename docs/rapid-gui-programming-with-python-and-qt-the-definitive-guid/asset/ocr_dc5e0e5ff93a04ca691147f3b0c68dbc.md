central widget (which may contain other widgets, of course). We will look at main window-style applications in Chapter 6.

![](bbox=[0.32, 0.14, 0.68, 0.36])

This application uses two widgets: A QTextBrowser which is a read-only multi-line text box that can display both plain text and HTML; and a QLineEdit, which is a single-line text box that displays plain text. All text in PyQt widgets is Unicode, although it can be converted to other encodings when necessary.

The Calculate application (shown in Figure 4.3), can be invoked just like any normal GUI application by clicking (or double-clicking depending on platform and settings) its icon. (It can also be launched from a console, of course.) Once the application is running, the user can simply type mathematical expressions into the line edit and when they press Enter (or Return), the expression and its result are appended to the QTextBrowser. Any exceptions that are raised due to invalid expressions or invalid arithmetic (such as division by zero) are caught and turned into error messages that are simply appended to the QTextBrowser.

As usual, we will look at the code in sections. This example follows the pattern that we will use for all future GUI applications: A form is represented by a class, behavior in response to user interaction is handled by methods, and the “main” part of the program is tiny.

```
from __future__ import division
import sys
from math import *
from PyQt4.QtCore import *
from PyQt4.QtGui import *
```

Since we are doing mathematics and don’t want any surprises like truncating division, we make sure we get floating-point division. Normally we import non-Py/Qt modules using the import module\*\*name syntax; but since we want all of the math module’s functions and constants available to our program’s users, we simply import them all into the current namespace. As usual, we import sys to get the sys.argv list, and we import everything from both the QtCore and the QtGui modules.

```
class Form(QDialog):
```