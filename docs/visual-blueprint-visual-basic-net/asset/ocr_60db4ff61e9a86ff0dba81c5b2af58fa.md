# Extra

You use the argument list of a property to access data values of a list or array the class stores. You can also make a property with an argument the default property of the class. If the property is the default, you can access it by typing the name of the class, followed directly by the index in parentheses without specifying the property name.

You can create properties that only support reading their value or only support writing to the property using the ReadOnly and WriteOnly keywords before the Property keyword.

# Example:

```
Private myData(10) As String
Default Public Property Data(ByVal Index As Integer) As String
    Get
        If Index >= 0 And Index <= 10 Then Return myData(Index)
    End Get
    Set(ByVal Value As String)
        If Index >= 0 And Index <= 10 Then myData(Index) = Value
    End Set
End Property
```

# Example:

```
Public ReadOnly Property ReadMe()
    Get
        Return myData
    End Get
End Property
Public WriteOnly Property WriteToMe()
    Set(ByVal Value)
        myData = Value
    End Set
End Property
```

![](bbox=[0.07, 0.53, 0.48, 0.82])

![](bbox=[0.52, 0.53, 0.93, 0.82])

VB .NET creates the full property block including Get and Set blocks.

+   5 In the Get section of the Property, type Return.

+   6 Type the private member variable name.

+   7 In the Set section of the Property, type an If statement to validate the Value variable.

+   8 Type the name of the private member variable.

+   9 Type = Value.

The property is complete.

Note: See "Using an Existing Class" for more on properties in your custom class.