# Extra

In some cases, you may want to place code for controlling the RadioButton or CheckBox control inside a separate event, rather than handling it in a button that accepts changes in the form. You can use the CheckedChanged event of both controls to monitor changes to the Checked property. The event is a non-post-back event, so the event stores and fires as soon as the user invokes an event that requires a server connection, like clicking a button.

You may want to know immediately when the user clicks one of the controls. Normally, VB .NET saves the event and fires it along with a post-back event to cause fewer round-trip connections to the server, which can consume a significant amount of time and interrupt the user. You can use the AutoPostBack property to enable post-back behavior for this control. When you set AutoPostBack to True, the CheckedChanged property causes the browser to submit the page to the server, allowing your event to fire and a new page to generate.

![](bbox=[0.06, 0.5, 0.52, 0.82])

![](bbox=[0.52, 0.5, 0.94, 0.82])

+   6 Double-click the Checked property to toggle it to True for appropriate controls.

+   7 Edit any optional properties.

+   8 Run your project by pressing F5.

For radio buttons, only one radio in a group can have Checked = True.

The option buttons respond to user input and let you make selections.