# CREATE A WINDOWS FORMS CONTROL

You can create a Windows Forms user control into which you can add a set of controls for reuse throughout a project. Alternately, you can place the control in a library to use in multiple projects. The UserControl object provides the ability to design your own controls.

When you add a user control to a project, the Windows Control Designer, similar to the Windows Forms Designer, gives you a designer space without a title bar. You can use the Toolbox to add any number of controls to the user control. For more information on designing a user control by combining standard Windows form controls, see the section "Using Standard Controls."

You can also use the UserControl object's events that the control inherits from to paint onto the service and create your own user control that does not rely on combining other controls. This capability lets you create any sort of control by providing a custom painting method and your own event model. For more information on creating a control without using standard controls, see the section "Create a Control from Scratch."

To name a control that you create, change the Name property of the UserControl object. The Name property modifies the class name, so this name functions as the default name of the control that displays in the Toolbox when you add the user control to a form.

If you want to use a control, or a set of controls, in multiple projects, you can create a Windows Control Library project to hold the controls. When you create this project, VB .NET builds a .NET-compliant DLL that you can reference in other projects. To create a Windows Control Library project, you select the template from the Add Project dialog box. The name you give the project functions as the name of the assembly for referencing. The template provides one UserControl automatically, but you can add any number of controls to the project.

# CREATE A WINDOWS FORMS CONTROL

![](bbox=[0.05, 0.58, 0.45, 0.78])

![](bbox=[0.52, 0.58, 0.92, 0.78])

+   1 Open a Control Library or Windows Application project.
+   To create a Control Library project, select the Windows Control Library template when you create a project.

+   2 If you are using a Windows Application project, click Project → Add User Control.
+   The Control Library project already contains a UserControl you can use.

+   3 Type a name for the new user control.
+   The Add New Item dialog box opens.

+   4 Click Open.