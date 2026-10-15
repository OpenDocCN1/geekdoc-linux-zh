
## PROVIDE ERROR MESSAGES

You can use the ErrorProvider control to alert a user to a data entry error by displaying an unobtrusive small error icon. The ErrorProvider control allows you to show an error message related to a control without bringing up a message box that stops the user’s flow of information entry. The ErrorProvider provides three properties to all of the controls on a form that allow you to monitor the controls for errors. The properties the provider adds to controls are Error, IconAlignment, and IconPadding. Typically, you use the ErrorProvider with text box controls because they provide a free-flow information entry area that can easily contain errors.

The Error on ErrorProvider property allows you to set an error message to appear for the control. Placing a string into this property makes an error icon appear beside the control. When the user moves the mouse over the icon, a tool tip pops up with the error text specified in the property. In most cases, you do not want to set the error at design-time and instead want the error icon to appear dynamically when an error occurs.

The SetError method allows you to set the error message for a control at runtime. Its first argument is the control where the error exists, and the second is the error text, for example, SetError(TextBox1, "Error Message"). You use this method when doing validation on a control.

Controls on the form provide a Validating event that each control raises after the user moves to another control. This event allows you to check the value of the control for errors. If you find an error with a selection, set the error text using the SetError method. If the user fixes the error, clear the message by calling the method with a blank string for the error message.

![](img/d6f772854306e15fb6df39b861a7b541_95_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_95_1.png)

- 1 Create a new Windows Application project or open an existing one
- 2 In the Toolbox, double-click the ErrorProvider control.
- The control appears in the component tray.
- 3 Add an input control to the form and another control to move the focus so validation occurs.
- The example adds a TextBox control and a Button control on the form.
- 4 Right-click the form and click View Code.
- The Code Editor appears.
- 5 In the class list, select the input control you added.
- 6 In the event list, select the Validating event.
- VB .NET creates the event handler.
- 7 Type code to check for an input error.

## Extra

You can specify the IconAlignment property the ErrorProvider control adds to each control to customize the location of the error icon on the form. The IconPadding on ErrorProvider property allows you to set the number of pixels between the control and the icon. Remember to be careful of the spacing you set. You should not add so much spacing it is hard to distinguish which icon relates to which input control. A useful feature of this property is to make all of your error icons line up in a column running down the screen beside the controls, even if the controls are not all of the same length.

Some properties are available in the ErrorProvider control itself that allow you to control the appearance of the icon that appears beside the input controls. The Icon property allows you to change the error icon you display. You can assign any icon file to this property. You can also set the BlinkStyle property to manipulate the blinking properties of the icon. You can set the property to AlwaysBlink, which makes the icon blink until the user corrects the error message, NeverBlink to ensure the error icon never blinks, or the default, BlinkIfDifferentError, which blinks only if the error message changes.

![](img/d6f772854306e15fb6df39b861a7b541_96_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_96_1.png)

- 8 To set the error message, type the name of the ErrorProvider control followed by .SetError().
- 9 Inside the parentheses, specify the input control followed by a comma and the error message in quotes.
- 10 To clear the error message, follow steps 8 and 9 but enter a blank error message.
- 11 Press F5 to run the project.

An alert icon appears beside the control when validation fails and your text appears when a user holds the mouse over it.
