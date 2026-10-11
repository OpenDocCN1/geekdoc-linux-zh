![](bbox=[0.08, 0.05, 0.92, 0.26])

![](bbox=[0.08, 0.27, 0.92, 0.45])

There are a variety of different options that can be passed to these dialogs, allowing you to set the allowable file types, default filename, and more. These are detailed in the getOpenFile/getSaveFile and chooseDirectory reference manual pages.

# Selecting Colors

There is also a modal dialog to let the user select a color. It will return a color value, e.g. “#ff62b8”. The dialog takes an optional “initialcolor” option to specify an existing color that the user is presumably replacing.

```
from tkinter import colorchooser
colorchooser.askcolor(initialcolor='#ff0000')
```

![](bbox=[0.08, 0.64, 0.92, 0.87])