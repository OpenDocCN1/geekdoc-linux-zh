# Extra

You can use the events available to the TrackBar control to make mouse scrolling an effective method of scrolling through values of the control. If the user moves the slider using a mouse wheel, the control does not raise the Scroll event. Instead, the control raises the MouseWheel event. You can call the Scroll event from the MouseWheel event to perform the same functionality.

You can manipulate properties to allow the user to move easily through the range of values. The SmallChange property specifies the smallest increment the slider moves. You use this to decide what values the slider moves to when the user drags it. For example, a value of two only allows the user to select every other number when moving the tracker. The LargeChange property determines how much the slider moves when the user clicks on the bar or uses the page up and page down keys to the sides of the slider.

# Example:

```
Private Sub TrackBar1_Scroll(ByVal sender As _
    System.Object, ByVal e As _
    System.EventArgs) Handles TrackBar1.Scroll
    Label1.Text = TrackBar1.Value.ToString()
End Sub
Private Sub TrackBar1_MouseWheel(ByVal sender As _
    Object, ByVal e As _
    System.Windows.Forms.MouseEventArgs) _
    Handles TrackBar1.MouseWheel
    TrackBar1_Scroll(sender, e)
End Sub
```

![](bbox=[0.06, 0.52, 0.5, 0.815])

![](bbox=[0.5, 0.52, 0.93, 0.815])

The Code Editor appears.

8 To retrieve the TrackBar value on the form, type the name of the control followed by .Value.

9 Press F5 to run your program.

The user can move the bar around as necessary.