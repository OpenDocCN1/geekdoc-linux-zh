
## Extra

You can use labels, frames, groups, and other visual cue components to enhance tab order just like input controls. For example, a label to the left of a control has Text equal to Name: and a text box is located directly to the right of it. You must add an access key to each label, so the label has the text &Name:. Then the user can press Alt+N. A label focuses on the control with the next tab index when you press the access key. It is important to set the TabIndex of the label, then the corresponding input control.

Both GroupBox and Panel contain other controls. You must set a container control’s TabIndex to the number before the top-left control in the container. The title of a GroupBox acts like a label and passes focus to the first control inside the container. When numbering controls inside of a container, follow the same system as numbering the form. Start at the top-left of the container, and work your way through the entire container moving either right or down. You should not make the order pass out of the container and back into it later, as this may confuse the user.

![](img/d6f772854306e15fb6df39b861a7b541_64_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_64_1.png)

- 7. Click the next control (either to the right or below).
- 8. Set the TabIndex to the next highest index.
- 9. Repeat steps 7 and 8 until you set the TabIndex for all of the controls.
- 10. Press F5 to run the project.
- 11. Experiment using the Tab key to navigate your form.

The controls follow the order given with the TabIndex property.

## USING BUTTONS

You can use buttons to provide simple user input in your application. A button represents a single action verb, such as accept, cancel, or go. This simplicity makes it effective in that most users understand the purpose of buttons.

You primarily use buttons on dialog boxes, and not normally on the main application screen. Instead of individual buttons, you may want to use a toolbar on the main window. See the section “Create a Toolbar” later in the chapter for more information.

The Button control has a variety of properties to change its appearance. The FlatStyle property allows you to create flat-style buttons. Flat buttons change color when a user moves over or clicks them, but have no three-dimensional effect. The Popup style makes the button appear flat. It takes on a raised three-dimensional appearance when the user moves the mouse over it, and depresses when a user clicks it. The Standard style appears raised in all cases, and depressed when the user presses the mouse button.

You can load a background image into the button by setting the BackgroundImage property to a supported format. You place images in the foreground with the Image property. You can also load images from ImageList controls with the use of two properties, ImageList and ImageIndex. See the section “Work with ImageLists” for more information.

You use the ImageAlign property to set the image alignment to the middle, edge, or corner of the button. You use the TextAlign property to align the Text in the same way.

To respond to the user pressing the button, you can create an event handler that responds to the Click event. For more information on creating event handlers, see the section “Add an Event.”

![](img/d6f772854306e15fb6df39b861a7b541_65_0.png)

- 1. Create a new Windows Application project or add an existing one.
- 2. In the Toolbox, click and drag the Button control to add it to the form.
- 3. In the Properties window, set the Text property to change the button caption.
- 4. Change any necessary properties.
- 5. This example sets the FlatStyle to Popup.

> Note: See Chapter 2 to learn about creating Windows Application projects, and adding a control to a form.

> Note: See Chapter 2 to set a property or create an event handler to respond to the Button’s Click event.

## USING LABEL CONTROLS

Labels provide information on the form to guide the user. You add a label control to provide an explanation of information the user needs to supply on the form or to explain information available on the form. A form often presents the user with various controls that contain data or lists of information, or blank controls waiting for user input, which make the labels necessary to describe the nature of the controls.

Try to make labels short, but descriptive. Most labels have a colon after the text to signify the label describes the control to the right or bottom of it. Refrain from placing labels to the right or below the control they describe.

Use the Text property to modify the text that label displays, and TextAlign allows you to align the text to the middle, side, or corner of the label. The AutoSize property, when set to True, automatically stretches the label’s width to fit the text you place on it. This prevents the text from wrapping at the edge of the control.

The LinkLabel control expands on the capability of the Label control by providing an appearance of a hyperlink. By setting the LinkVisited property to True, you can cause the link to appear in the visited color. Just like a Web page, you can set this property and cause the link to appear visited after the user clicks the link.

For the LinkLabel control, the LinkArea property specifies a range of text you want to use as the hyperlink. By default, the entire text of the control is used. Set the Start property to the character position to start the hyperlink, and set the Length property to the number of characters that you want as part of the link. When you set the Start property, remember the first text position is zero. The control fires the LinkClicked event if the user clicks on the area of the control that is part of the link.

![](img/d6f772854306e15fb6df39b861a7b541_66_0.png)

- 1. Create a new Windows Application project or open an existing one.
- 2. Click the Label or LinkLabel control in the Toolbox and add the control to the form.
- 3. In the Properties window, set the Text property of the control.
- 4. Press F5 to run your project.

The Label control provides textual information on the form.

- For the LinkLabel control, you can handle the user clicking the link in the LinkClicked event.

> Note: See Chapter 2 to add an event handler.
