# Extra

Although you can have any number of forms in a single project, only the default form appears automatically when you run the project. Different from previous versions of Visual Basic, you must create an instance variable of a form before showing it in VB.NET. Because the form that the Designer creates is nothing more than a class, you need to create an instance of the class. See Chapter 5 for more on creating classes.

# Example:

```
Dim frm As New Form1
frm.Show()
```

You can alter the size of a form simply by selecting the form in the Form Designer and dragging the handles that appear. However, you cannot visually specify where you display the form.

By default, the StartPosition of the form is WindowsDefaultLocation. You can have the form start in the center of the screen by setting this property to CenterScreen. You can also place it precisely by setting StartPosition to Manual and filling the Location property's Point. A Point is comprised of an x, y location.

You limit the size the form can resize by using the MinimumSize and MaximumSize properties. Fill in the Point with a width and height and the user cannot resize the window out of these bounds, even though you limit maximizing to the MaximumSize property.

![](bbox=[0.06, 0.56, 0.94, 0.83])

6 Click in the Startup object box and click Form2.

7 Click OK.

8 Press F5 to run your project.

The new form displays and the original form does not.