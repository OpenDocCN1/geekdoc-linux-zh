# Apply It

You can create a progress meter that updates inside a single panel of your status bar. To create custom panels, set the panel’s Style to OwnerDraw. When this is set, the StatusBar control fires the DrawItem event every time you need to redraw the panel. If you want to manually redraw the panel, you can use the Invalidate method. In the example below, place the percentDone declaration at the top of the form code. Add a button to the form and set one panel’s Style = OwnerDraw. When you press the button, the progress meter fills by 5 percent.

# TYPE THIS:

```
Private percentDone As Integer

Private Sub StatusBar1_DrawItem(ByVal sender As Object, ByVal e As System.Windows.Forms.StatusBarDrawItemEventArgs) Handles StatusBar1.DrawItem
Dim g As Graphics = ebdvent.Graphics
Dim b As Brush = New SolidBrush(SystemColors.Highlight)
Dim rect As Rectangle = ebdvent.Bounds
rect.Width = CInt((CInt(percentDone) / 100 * rect.Width))
g.FillRectangle(b, rect)
End Sub

Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
percentDone = percentDone + 5
StatusBar1.Invalidate()
End Sub
```

# RESULT:

The progress bar panel fills when a user repeatedly clicks the button.

![](bbox=[0.06, 0.56, 0.94, 0.82])

7 Click Add to create a new panel.

8 Type text to display into the Text property.

9 Modify the width of the panel by typing a value into the Width property.

10 Edit other properties as desired.

11 Repeat steps 7 through 10 as necessary, clicking OK to accept changes.

The StatusBar appears with the appropriate interface.