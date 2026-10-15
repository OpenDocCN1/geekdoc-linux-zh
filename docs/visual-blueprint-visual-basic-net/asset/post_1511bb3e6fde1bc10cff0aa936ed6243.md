
## Extra

Many of the tasks in this chapter expect you to use the Property Window to make changes to the forms and controls. In some cases, you may find this window difficult to find with the large number of tool windows present at any time on the screen. You can access the Properties window by clicking the View menu and selecting Properties window from the menu or by pressing the F4 key.

You can use the Class View window to receive a representation of forms and other classes in your project instead of using the Solution Explorer window. The Class View window enables you to see the members, such as properties, methods, and events that make up all of the classes in the project, and jump directly to specific areas of code inside a module. By right-clicking a class inside the window, you can change view and sort options. For example, the Group by Type option enables you to show the members that make up the class in separate trees, splitting off private variables and public members. To show this window, go to the View menu and click Class View.

![](img/d6f772854306e15fb6df39b861a7b541_40_0.png)

- The New Project dialog box appears.
- Click Visual Basic Projects if it is not currently selected.
- Click Windows Application Project.
- Type a name for the project.
- Click OK.

The Development Environment creates a project directory and a default Form1 that loads into the client area.

## AN INTRODUCTION TO WINDOWS FORMS

You can use Windows Forms, a large technology encompassing a huge set of tools, to build powerful Windows applications quickly and easily. In this chapter, topics cover creating forms, manipulating forms, and adding controls to those forms.

To understand the capabilities of a form, see the summary of important Form members given below. A member refers to any part of a component in VB.NET available for your manipulation or viewing. Forms, controls, and classes all have a set of members such as properties, methods, and events that give them their ability to perform certain tasks. For more information on object-oriented terms, see Chapter 7.

A Form provides the backdrop where all of your application’s abilities are accessible. Controls provide the functionality on the form, enabling the user to view, edit, manipulate, and explore your application. A control is anything that you place onto a form, like a button, or a list box, or a check box. To learn how to add controls to your form, see the “Add a Control” section.

The tables below do not include all of the abilities of a form, but touch on some of the abilities that you may find interesting or useful. Many members that are shown here are covered more fully throughout the chapter. For more information on setting a form’s properties, see the section “Set a Property.” For more information on responding to a form’s events, see the section “Add an Event.”

## IMPORTANT FORM MEMBERS

| PROPERTIES | DESCRIPTION |
|---|---|
| AcceptButton | Set this property to a Button control that automatically activates when the user presses Enter. The AcceptButton only activates if the current control uses the Enter key, like a multi-line text box, the current control uses the key press and the button does not receive the click event. |
| AutoScale | Makes the form and its controls automatically resize to fit user font-size preferences. You may want to change this to False for proprietary interfaces not using standard controls. |
| AutoScroll | When True, AutoScroll adds scrollbars to the form when all of its constituent controls do not fit. |
| BackgroundImage | Loads an image into the form’s background. The image tiles across the entire form. Supports a large number of formats, including BMP, GIF, JPEG, PNG, WMF, and others. |
| CancelButton | See the description of AcceptButton above, except CancelButton functions on the Esc key. |
| FormBorderStyle | Sets the border of the window. The default setting is Sized, which allows resizing. You use the FixedDialog setting to create a fixed window that looks like a dialog box. Fixed3D creates a fixed window with a sunken client area. |
| Location | This property determines the position of the window on the Desktop. Windows automatically corrects it depending on the position of the Taskbar. You need to set StartPosition to Manual for Location to work. |
| MaximizeBox | Determines whether the form displays a maximize button in the title bar. |
| MaximumSize | A Point object specifying the maximum width and height the form reaches. Beware: This is also in effect when you maximize the form. |
| Menu | Determines which MainMenu control actually provides the menu interface for the window. |
| MinimizeBox | Determines whether the form displays a minimize button in the title bar. |
