This program displays the dialog box previously shown in Figure 3-1, and also displays the window shown in Figure 3-3. Lines 10 through 20 create and display the main window and its button. While both the main window and the dialog are being displayed, only the button in the dialog box responds to the mouse because of the call to gtk_window_set_modal() on line 20. The button in the main window ignores the mouse until the OK button of the dialog box is clicked and the dialog closes. After that, the main window button works normally.

![](bbox=[0.11, 0.29, 0.21, 0.38])

# Figure 3-3: The button of the main window

Lines 15 and 16 display the button and app widgets. In this example, the button widget is displayed before its parent, the app widget. If the order of the calls to gtk_widget_show() is reversed, the end result is the same—but the process of painting the widgets on the screen is different. I discuss more about this later in the chapter.

The code on lines 18 through 20 that creates and displays the dialog does not require the app window as an argument. This means that a dialog easily can be created from any point in your program and can halt all window activity within the application until the dialog is acknowledged.

The calls to gtk_widget_show() on lines 15 and 16 can be in any order. The fact is that the button widget does not display at all if the app widget is not being displayed also, because the call to gnome_app_set_contents() on line 14 places the button inside the app widget. Generally speaking, it is better to display the widgets from the inside out this way because the entire window and all its widgets will appear at once. In a large window—one that contains lots of widgets—if the outer window is displayed first, the widgets can all appear one at a time after the containing window first appears.

Up until now, the dialog window has been a free agent and the mouse could place it either in front or behind any of the other windows on the display. This example shows that if the dialog has a parent window, it always remains in front of the parent. This seems to make especially good sense when using modal dialogs, because the parent window is inactive anyway and hiding the dialog could cause confusion. You can alter the program by changing lines 18 and 19 to this:

```
dialog = gnome_ok_dialog_parented( 
  "A simple information window", 
  GTK_WINDOW(app));
```