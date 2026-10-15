# DEVELOPING COMPONENTS

# Apply It

You can provide drawing functions that appear like the popup style of the `Button` control. To monitor for the user pressing the mouse in the `UserControl`, set a state variable in the `MouseDown` event handler and the `MouseUp` event handler when the user lets go of the mouse button. You can use the `MouseEnter` and `MouseLeave` event to monitor the user entering or exiting the control, which you can use to provide a popup-style appearance.

```
Private Enum ButtonState
    Normal
    Pressed
    Hover
End Enum
Private myState As ButtonState = ButtonState.Normal

Private Sub UserControl1_MouseDown(...) Handles MyBase.MouseDown
    myState = ButtonState.Pressed: Me.Invalidate()
End Sub
Private Sub UserControl1_MouseEnter(...) Handles MyBase.MouseEnter
    myState = ButtonState.Hover: Me.Invalidate()
End Sub
Private Sub UserControl1_MouseLeave(...) Handles MyBase.MouseLeave
    myState = ButtonState.Normal: Me.Invalidate()
End Sub
Private Sub UserControl1_MouseUp(...) Handles MyBase.MouseUp
    myState = ButtonState.Normal: Me.Invalidate()
End Sub
```

# TYPE THIS:

# RESULT:

The control responds graphically to the user’s mouse.

![](bbox=[0.072, 0.534, 0.499, 0.821])

![](bbox=[0.519, 0.534, 0.946, 0.821])

+   4. Add necessary events, properties, and methods to the control.

+   5. Select (Base Class Events) in the component list and select the Paint event.

+   6. Type code to paint the control.

+   7. Build the control.

The control draws itself and functions like a standard control when you add it to a form.

> Note: To add properties and methods, see “Add a Member.” To add events, see “Add an Event.” To build a project, see Chapter 1.

> Note: To reference a control in a control library, see “Reference a Library.”