the full text from the items in the case options. If there are any spaces in the text, you need to use quotation marks around the text. Using the zenity package, you can add a Windows feel to your interactive shell scripts in the GNOME desktop.

# ## Working Through a Practical Example

The one downside to each of these graphical packages is that there isn't a way to create a window with multiple entries, such as combining several text box inputs along with a calendar input, as you can do in a true graphical environment. That limitation does make querying for multiple data items a bit clunky, but it's still manageable. The trick is to keep track of each data query using appropriately named variables.

The dialog package does include a form feature, but it's fairly elementary. It only allows you to combine several text boxes into a single window to enter multiple data items. The format for the --form option is

```
```
--form text height width formheight [ label y x item y x flen  ilen ] ...
```
```

The parameters used by the --form option are as follows:

+   - *text*: A title that appears at the top of the form
+   - *height*: The total form window height
+   - *width*: The total form window width
+   - *formheight*: The total height of the form within the window
+   - *label*: The label for the form field
+   - *y*: The Y position of the label or item within the form
+   - *x*: The X position of the label or item within the form
+   - *item*: A default value to assign to a form field
+   - *flen*: The length of the form field to display
+   - *ilen*: The maximum length of the data that can be entered into