# Extra

While automatic resizing using Anchor and Dock is very powerful, you may find that this does not meet your needs for a complex or custom-designed form. In this case, VB.NET provides a more sophisticated system. You can resize all of your controls by hand by using the Resize event. This event is called whenever you resize, maximize, minimize, or restore the form. Simply use the form's dimensions, which you can retrieve using the Size.Width and Size.Height members of the form. Then move and resize the controls accordingly. You can move a control by editing its Location.Left or Location.Top properties, or reassigning the entire Point structure by using Location = New Point(Left, Top). Utilize Size.Width and Size.Height to resize the control, or use a Size structure like Size = New Size(Width, Height). You can also use the manual resize event for some controls, and Anchor and Dock for others. Be careful when a user minimizes the form, or happens to make the form very small, because your calculated values may create negative values for width and heights and cause your program to have a run-time error.

# SPREAD TO FORM DIMENSIONS

+   6 Add a control to the form.
+   7 Size the control to take up the remaining space on the form.

+   8 Set the Anchor property to Top, Bottom, Left, Right.
+   9 Run the project by pressing F5.

When you resize the form, everything sizes properly.

![](bbox=[0.07, 0.475, 0.56, 0.75])

![](bbox=[0.56, 0.475, 0.93, 0.75])