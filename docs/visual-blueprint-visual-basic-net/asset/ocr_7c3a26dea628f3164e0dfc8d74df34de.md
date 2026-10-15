# Extra

Shared variables that you declare in your classes sometime initialize during program execution. VB .NET does not specify a single point to execute them, only that they initialize before you create an instance of the class or access a shared variable. VB .NET guarantees they only initialize once. You can create shared constructors to initialize the values of the shared variables. A shared constructor does not support any parameters, because VB .NET calls it directly. Declare a new constructor and place Shared before the Sub New statement. You can only initialize shared variables in this constructor.

# TYPE THIS:

```
Public Class Class1
    Public Shared Variable1 As Integer
    Shared Sub New()
        Variable1 = 5
    End Sub
End Class
Public Class Form1
    Inherits System.Windows.Forms.Form
    Sub Form1_Load(...) Handles MyBase.Load
        MsgBox(Class1.Variable1)
    End Sub
End Class
```

# RESULT:

5

![](bbox=[0.07, 0.55, 0.48, 0.86])

4 Where you need to use the variable, type the name of the class holding it.

5 Type a period followed by the name of the shared variable to access.

6 Type a value for the variable.

7 Press F5 to run your project.

![](bbox=[0.52, 0.55, 0.94, 0.86])

The shared variable holds the value without an instance of the class existing.