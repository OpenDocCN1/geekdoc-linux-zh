# Responding to buttons

A Button widget provides a graphical button in an application window that may contain either text or an image to convey the button’s purpose. A button object is created by specifying the window name and options as arguments to a Button() constructor. Each option is specified as an option=value pair. The `command` option must always specify the name of a function or method to call when the user clicks that button. The most popular options are listed below, together with a brief description:

| Option: | Description: |
| :--- | :--- |
| activebackground | Background color when the cursor is over |
| activeforeground | Foreground color when the cursor is over |
| bd | Border width in pixels (default is 2) |
| bg | Background color |
| command | Function to call when clicked |
| fg | Foreground color |
| font | Font for button label |
| height | Button height in text lines, or pixels for images |
| highlightcolor | Border color when in focus |
| image | Image to be displayed instead of text |
| justify | Multiple text lines as LEFT, CENTER, or RIGHT |
| padx | Horizontal padding |
| pady | Vertical padding |
| relief | Border style of SUNKEN, RIDGE, RAISED or GROOVE |
| state | Enabled status of NORMAL or DISABLED |
| underline | Index number in text of character to underline |
| width | Button width in letters, or pixels for images |