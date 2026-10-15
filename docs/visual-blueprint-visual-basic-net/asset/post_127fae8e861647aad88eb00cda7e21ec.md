
## USING WEB CONTROL LIBRARIES

You can use a Web control project to generate a DLL of Web custom controls for use on Web Forms pages. Unlike a Web user control, you add Web custom controls to a Web control library. These controls appear as actual entries in the Web Forms toolbox and do not reside on an ASP.NET page of a Web project. A Web custom control functions exactly like the existing controls that VB .NET provides.

When you create a custom control, you create your very own custom control, therefore preventing you from combining existing controls like you would in a Web user control. To create a Web custom control, you must specify exactly how the control generates on the Web Form page.

You use standard HTML output to generate the appearance for your control. To output this code, you override the Render method provided by the WebControl base class. The method has a single parameter of type HtmlTextWriter, which enables you to write to the page with the object's Write method.

You define properties, methods, and events like any other class or control. See the section "Add a Member" for information on adding properties and methods to a control. Use private member variables to hold data for the control. The Web Forms system maintains the state of the object automatically.

When you create a Web Control Library project, the template contains one custom control. The control in the template predefines a Text property and outputs the text in its Render method. You can delete this property and alter the Render method, but the template provides a good starting point for building your control. To reference the Web Control library in a Web Application project, add a reference and customize the Toolbox as you might when using a Windows forms control library. For more information on referencing a library, see the section "Reference a Library."

## USING WEB CONTROL PROJECTS

![](img/d6f772854306e15fb6df39b861a7b541_313_0.png)

## CREATE A WEB CONTROL LIBRARY PROJECT

- 1. Open the New Project dialog box.
- 2. Click Visual Basic Projects.
- 3. Click the Web Control Library template.
- 4. Type a name for the project.
- 5. Click OK.

Note: To create a new project, see Chapter 1.

The Code Editor appears with a default Web custom control class open.

- 6 Define properties, methods, and events for the control.

If desired, you can remove the code for the default Text property and the default code from the Render method.

Note: To define methods and properties, see "Add a Member." To define events, see "Add an Event."

## Extra

You can add information to your properties for the visual forms designer if you desire. To add template information, use angle brackets (<>) before the definition of either the class or a particular property or event. You can find a reference for most of the standard template properties in the section “Create a Component.”

```
**Example:**

```vb
<Bindable(True), Category("Appearance"), DefaultValue("")> _
Property Text() As String
    Get
        Return mText
    End Get

    Set(ByVal Value As String)
        mText = Value
    End Set
End Property
```
```

The WebControl class forms the basis of your custom control in a Web control library. The WebControl class exports a number of properties for all controls, much like the Windows forms Control class. You can override these properties if you want them to function in a particular way. See “Handle Default Properties” to learn how to override properties and events of the base control. For a reference of the properties a WebControl, search Visual Basic .NET help by typing WebControl members.

Because you cannot use other controls to build a Web custom control, if you want to post-back for certain events, you must provide the function yourself. For more information on generating post-back events, see the section “Create a Web User Control.”

![](img/d6f772854306e15fb6df39b861a7b541_314_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_314_1.png)

## RENDER THE CONTROL

- 7. In the Render method, type `output.Write()`, replacing output with the HtmlTextWriter object's variable name and placing a string of data to export from the control inside the parentheses.
- 8. Repeat step 7 as necessary.
- 9. Build the control library.

- The default definition declares the variable as output.
- The control is complete.
- You can reference the control in a Web Application project and add it to the page.

> Note: To build a project, see Chapter 1.

> Note: To reference the Web control library, see “Reference a Library.” To use Web forms, see Chapter 10.
