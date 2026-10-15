# Extra

You can receive a number of common errors when you work with the Visual Basic language. You can use the following list to decipher the meaning of some of these errors. For more help with error messages, press F1 with an error selected in the Task window.

| ERROR MESSAGE | HOW TO CORRECT |
|---|---|
| The name 'x' is not declared. | The compiler cannot locate the variable or method name. Ensure that you declare the variable in question at the appropriate scope for the line of code to access it. Commonly, this error message displays because of a spelling error. |
| Expected an expression. | A line did not end appropriately. In some cases, this can cause a multitude of errors as VB.NET tries to find the end of line. Make sure open and close parentheses match and that you do not have an underscore on the last line of a multi-line command. |
| A value of type 'x' cannot be converted to 'x' | You assign a value to a variable that cannot accept it. This occurs often if you try to assign information to a control, for example, when you assign a string to a Label or TextBox control without specifying the Text property. |

![](bbox=[0.06, 0.5, 0.48, 0.8])

![](bbox=[0.52, 0.5, 0.94, 0.8])

# RUN A PROJECT

3 Click Debug → Start.

Alternately, you can press F5 to access the Start function.

The project starts under the control of the .NET debugger.

Any run-time errors cause the debugger to stop execution of the program and to display an error message.