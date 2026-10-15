# Extra

You can add read-only methods to your component, control, or class to provide information to the control's container. If your control maintains a collection of objects, you can use a ReadOnly property to allow access to the items without allowing direct changes to the objects.

```
```vb
Private items As New Collection()
Public ReadOnly Property Item(ByVal index As Integer)
Get
Return items(index)
End Get
End Property
Public Sub Add(ByVal item As Object)
items.Add(item)
End Sub
```
```

You can make your property take on a range of values specified by an enumeration of constants using the Enum block. Use the type name of the enumeration block for the property, and the designer loads the list and provides a drop-down list of constants.

```
```vb
Public Enum SelectionStyles
ByColor
ByName
End Enum
Public Property SelectionStyle() As SelectionStyles
...
```
```

# ADD A METHOD

+   1. Open an existing user control
+   2. Double-click the surface of the user control to go to the Code Editor.
+   3. On an empty line of the class, type Public followed by Sub or Function and the name of the method.
+   4. For a Function, add the return type after the As keyword at the end of the line, and then press Enter.
+   5. Type code inside the method to modify the function of the UserControl.
+   6. Click Build to build the control.

Note: To add methods to a class, see Chapter 4.