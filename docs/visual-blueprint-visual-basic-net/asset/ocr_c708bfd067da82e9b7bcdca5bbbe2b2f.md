# Extra

The UserControl also contains a number of default properties it inherits from the ContainerControl class, which is the class that lets controls contain other controls inside of it. The ContainerControl inherits from ScrollableControl, which inherits from Control to provides the basic functions of all parts of the Windows Forms hierarchy. Properties such as BackColor, ForeColor, Tag, Enabled, and AutoScroll automatically apply to your user control through the various class that the UserControl inherits from. For more information on how to handle and override these built-in properties, see the section “Handle Default Properties.”

Unlike Visual Basic, you cannot create a UserControl that the user utilizes as a container. When developing the UserControl, you can add any necessary properties. The user cannot add controls to the UserControl, so you cannot replicate the function of a GroupBox or Panel control. You may want to create your own versions of these container controls directly instead of building a UserControl. To inherit from existing controls, search Visual Basic help by typing Inherit from existing Windows Forms Controls.

![](bbox=[0.072, 0.499, 0.498, 0.785])

![](bbox=[0.51, 0.499, 0.948, 0.785])

+   5. The visual designer for the new control appears.
+   
+   6. Add any necessary controls to the visual designer.

Note: See the section “Using Standard Controls” to add controls to the UserControl.

+   6. In the Code Editor, add necessary members to the control.

Note: See the section “Add a Member” to add class members to the control.

+   7. Click Build ↔ Build to make the control or library usable.
+   
+   8. If the control exists in a control project, you can now reference the library. If you created the control in a Windows Application, go to a form and add it to the form.

Note: To reference a Control Library project, see the section “Reference a Library.”