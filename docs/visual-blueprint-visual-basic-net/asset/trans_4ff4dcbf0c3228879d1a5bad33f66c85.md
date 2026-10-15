

## 应用它

要创建一组协同工作的按钮列表，可以将列表中每个按钮的 CommandName 属性设置为同一个名称，并将 CommandArgument 属性设置为特定值。例如，在一个购物页面中，你可能有十个“添加到购物车”按钮。你可以将 CommandName 设置为 "AddToCart"，并将每个 CommandArgument 设置为产品的 ID。

### TYPE THIS:

```
Sub HandleCommandAction(ByVal sender As Object, _
    ByVal e As System.Web.UI.WebControls.CommandEventArgs) _
Handles Button1.Command, Button2.Command

If e.CommandName = "AddToCart" Then
    Dim productNumber As Integer = CInt(e.CommandArgument)
    Label1.Text = "You chose to buy product #" & productNumber
End If
End Sub
```

### RESULT:

You chose to buy product #145

![](img/d6f772854306e15fb6df39b861a7b541_254_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_254_1.png)

- The Click event loads in the Code Editor.
- Type code to specify an action for the button.
- The example changes the text displayed in a label control.

- Press F5 to run your application.
- Note: To work with label controls, see the section "Add a Label Control." For general coding tasks, see Chapter 4.

- Your Web Application responds to a button-click using your server-side code.

## ADD OPTION CONTROLS

You can create CheckBox and RadioButton controls for users to select on your Web Form. These controls function nearly identically to the controls with the same name in the Windows Forms Framework. The CheckBox control enables the user to select multiple check boxes on the form, while a RadioButton control allows the user to select only a particular control from the group.

You use the Text property to set text for both of the option controls. You can place HTML codes inside the Text property to create bold, italics, or various size fonts. The TextAlign property specifies if the text displays to the right or left of the check box or radio button, with the default being Right. You can use an option control with no text combined with an Image to provide selections for graphical items. If you choose an image, the text displays as a tooltip when the mouse rests over the image.

For the RadioButton control, the GroupName property specifies the name of the group for the control. Specify the same group name for a set of RadioButton controls to make them function together. If the user selects one of the items in the group, all of the other items in the group deselect.

For check boxes, you can use the Checked property to retrieve or set the check status of the control. If the form submits and the user selected an option control, the Checked of that option control property equals True.

To create a long set of either check boxes or radio buttons, you can use the CheckBoxList or RadioButtonList controls, which enable you to create one Web Forms control with an entire set of controls automatically. You can also bind the list control to a database to have a list of items created automatically. For more information, see the section "Work with Option List Controls."

![](img/d6f772854306e15fb6df39b861a7b541_255_0.png)

- 1 Create a new Web Application project or open an existing one.
- Note: See the section "Create a Web Application" to create a Web Application project.

- 2 Click either the CheckBox or RadioButton control in the Toolbox and add an appropriate number of the control to the form.
- Note: See the section "Using a Web Form" to add a control.

- 3 Click a control to select it.

- 4 Type a caption into the Text property.

- 5 Set the radio button or check box properties.

For a group of radio buttons, type the same group name for each of the controls you create into the GroupName property.

## Extra

In some cases, you may want to place code for controlling the RadioButton or CheckBox control inside a separate event, rather than handling it in a button that accepts changes in the form. You can use the CheckedChanged event of both controls to monitor changes to the Checked property. The event is a non-post-back event, so the event stores and fires as soon as the user invokes an event that requires a server connection, like clicking a button.

You may want to know immediately when the user clicks one of the controls. Normally, VB .NET saves the event and fires it along with a post-back event to cause fewer round-trip connections to the server, which can consume a significant amount of time and interrupt the user. You can use the AutoPostBack property to enable post-back behavior for this control. When you set AutoPostBack to True, the CheckedChanged property causes the browser to submit the page to the server, allowing your event to fire and a new page to generate.

![](img/d6f772854306e15fb6df39b861a7b541_256_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_256_1.png)

- 6 Double-click the Checked property to toggle it to True for appropriate controls.

- 7 Edit any optional properties.

- 8 Run your project by pressing F5.

For radio buttons, only one radio in a group can have Checked = True.

The option buttons respond to user input and let you make selections.

