|  | turned on or off |
|form| Allows you to build a form with labels and text fields to be filled out |
|fselect| Provides a file selection window to browse for a file |
|gauge| Displays a meter showing a percentage of completion |
|infobox| Displays a message without waiting for a response |
|inputbox| Displays a single text form box for text entry |
|inputmenu| Provides an editable menu |
|menu| Displays a list of selections from which to choose |
|msgbox| Displays a message and requires the user to click an OK button |
|pause| Displays a meter showing the status of a specified pause period |
|passwordbox| Displays a single text box that hides entered text |
|passwordform| Displays a form with labels and hidden text fields |
|radiolist| Provides a group of menu items where only one item can be selected |
|tailbox| Displays text from a file in a scroll window using the tail command |
|tailboxbg| Same as tailbox, but operates in background mode |
|textbox| Displays the contents of a file in a scroll window |
|timebox| Provides a window to select an hour, minute, and second |
|yesno| Provides a simple message with Yes and No buttons |

As you can see from Table 18.1, you can choose from lots of different widgets to give your scripts a professional look with little effort.

To specify a specific widget on the command line, use the double dash format:

```
dialog --widget parameters
```

where widget is the widget name as seen in Table 18.1 and parameters