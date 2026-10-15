# Apply It

You can fire an event that reports the percentage of the task that is complete. You can also allow the event handler to send information back to your class. The form can have a Cancel button whose handler code tells the method to stop when the event fires. A parameter with the ByRef keyword, which allows VB .NET to pass changes to the variable back when a routine finishes, make this possible.

# TYPE THIS:

```
Class LongTimeClass
Event PercentDone(ByVal Percent As Integer, ByRef Cancel As Boolean)
Sub DoWork()
Dim done As Boolean, cancel As Integer
Do Until done Or cancel ' do work in loop until done or user cancels
RaiseEvent PercentDone(percent, cancel) ' send new percentage
Loop
End Sub
End Class
Class Form1
Inherit System.Windows.Form
Private WithEvents workerClass As New LongTimeClass
Private CancelWork As Boolean = False
Private Sub CancelButton_Click(...) 
CancelWork = True ' user wants to cancel. tell class when event fires.
End Sub
Private Sub PercentDoneChanged(ByVal Percent As Integer, _
ByRef Cancel As Boolean) Handles workerClass.PercentDone
Application.DoEvents() ' you must update percentage bar here
If CancelWork Then Cancel = True ' cancel the work activity
End Sub
End Class
```

# RESULT:

The class method cancels work when a user presses the Cancel button.

![](bbox=[0.07, 0.58, 0.5, 0.85])

![](bbox=[0.5, 0.58, 0.93, 0.85])

5 Create or move to the method where the event fires.

6 Type RaiseEvent.

Note: To define a method, see Chapter 4.

7 Type the name of the event you previously declared and follow it with parentheses.

8 Type the values required by the parameter definitions and enclose them in parentheses.

The method raises the event when a user of your class calls it.

Note: See the section 'Using an Existing Class' for information on handling the event.