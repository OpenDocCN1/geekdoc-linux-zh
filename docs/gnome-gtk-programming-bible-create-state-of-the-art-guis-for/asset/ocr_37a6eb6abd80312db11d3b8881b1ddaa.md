This causes the app window to be the parent of the dialog. Any window can be the parent of one or more child windows, so you can use this same technique for popping up dialogs for any window in an application.

There are two other dialog windows that work the same way as the OK dialog window. The warning and error dialog windows both have parented and non-parented modes, and they both can be modal or non-modal. To display the error window shown in Figure 3-4, change lines 18 and 19 to this:

```
```
dialog = gnome_error_dialog_parented(
    "A simple error window",
    GTK_WINDOW(app));
```
```

![](bbox=[0.17, 0.35, 0.7, 0.48])

The third form of the simple OK popups is the warning, as shown in Figure 3-5. The display code follows the same form as the others:

```
```
dialog = gnome_warning_dialog_parented(
    "A simple warning window",
    GTK_WINDOW(app));
```
```

![](bbox=[0.17, 0.65, 0.7, 0.76])

# ### Ask a Simple Question

To get a yes or no answer from a dialog box, it is necessary to find out which of the two choices the user made. The response is captured with a callback function. Here is an example of a program that displays a question dialog box and captures the response: