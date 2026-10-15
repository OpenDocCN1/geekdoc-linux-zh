
```vb
Class ImplementClass Implements IInterface, Declarations

    Public Function Method1() As String

        ' Implements IInterface.Method1

        Return "method implemented"

    End Function

    Private _property10 As Integer

    Public Property Property10() As Integer

        Get

            Return _property10

        End Get

        Set(Value As Integer)

            _property10 = Value

        End Set

    End Property

End Class
```

implementsInterface - Microsoft Visual Basic, [Design] - `ImplementClass.vb`

File Edit View Project Debug Help

`Read1`

Model: `ImplementClass.vb`

```vb
Class ImplementClass Implements IInterface, Declarations

    Private _property10 As Integer

    Public Property Property10() As Integer

        Get

            Return _property10

        End Get

        Set(Value As Integer)

            _property10 = Value

        End Set

    End Property

    Event Event(Event Action As Integer, Cancel As Boolean) Implements IInterface.Event

    End Sub

End Class
```
