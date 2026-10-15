# Extra

When you create a shared method, which can only access other shared members, it does not run in the memory space of a class instance. You can fire an event from a shared method using shared events. To create a shared event, use the Shared keyword before the Event keyword when defining the event. In the class or module to handle the event, you use the AddHandler command to set up the method to handle the event. You can use this command for standard events as well as to dynamically handle events of a component. For the first parameter, specify the event. In the case of a shared event, type the class name, following it with a period and the name of the event. For a standard event, specify the instance variable name followed by a period and the event name. For the second parameter, type AddressOf followed by a method in the class or module to handle the event.

```
Example:
Public Class Class1
    Public Shared Event Event1()
    Public Shared Sub Method1()
        RaiseEvent Event1()
    End Sub
End Class
Public Class Class2
    Sub RunMethod()
        AddHandler Class1.Event1, _
            AddressOf HandleEvent
        Class1.Method1()
    End Sub
    Sub HandleEvent()
        ...
    End Sub
End Class
```

![](bbox=[0.071, 0.503, 0.499, 0.789])

![](bbox=[0.519, 0.503, 0.946, 0.789])

VB .NET creates the End Sub or End Function statement.

Type code for the shared method.

In the location that you need to use the method, type Math.Add(5, 10), replacing Math with the class name of the shared method, and 5, 10 with any necessary parameters.

Press F5 to run your project.

The shared method runs its code without the class being initialized.