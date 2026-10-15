
## Extra

## WORK WITH CONTROLS

You can specify a transparency color for the images in the control. The default setting for the TransparentColor property is Transparent, meaning it reads the transparency color from the image file, if the file type supports transparency. Icon files (ICO) and Graphics Interchange format (GIF) support transparency. If you load a collection of Windows bitmap (BMP) files into the ImageList control, set the TransparentColor to the appropriate background color of the images.

You can add images to the ImageList control at run-time using the Add method of the Images collection. Supply an Image object as the only parameter to the method.

**Example:**

```vb
' Visual Basic
' Replace string with valid image file path:
Dim myImage As System.Drawing.Image = _
    Image.FromFile("C:\sample.gif")
ImageList1.Images.Add(myImage)
```

![](img/d6f772854306e15fb6df39b861a7b541_68_0.png)

- 8. Add a control to display an image.
  - Controls such as the Button and Label control offer support for loading images from the ImageList control. The example adds a Button control.
- 9. In the Properties window, click the ImageList property and select the ImageList control.
  - You can clear the Text property to make the button appear with only an image.
- 10. Click the ImageIndex and select an image to display.

The ImageList provides the image to the control.

## ALLOW TEXT ENTRY

Text input is a vital part of most programs. You use a text box to allow users to enter freeform information that you cannot represent by a list of options. Notepad is an example of the functionality the standard text box provides. Without using text boxes for users to enter information, you must provide a selected set of options using check boxes, radio buttons, and lists.

Text boxes support two basic modes: single-line, and multi-line, which you can toggle. A single line input box is normally limited to a certain number of characters by the MaxLength property, with the maximum available size being 32767, and the height fixed at font and system settings. The Text property controls the text displayed by the TextBox control, and updates as the user enters new information in the control. You can create a password field in a single-line text box by specifying a character in the PasswordChar property. The character you specify appears instead of the actual information typed into the box. A normal value for the property is an asterisk (*).

You can make a multi-line text box can be any size, and have unlimited text up to the available memory. Use the ScrollBars property to assign horizontal, vertical, or both scrollbars to the multi-line text box. The WordWrap property, which defaults to True, controls whether the box wraps text at the edge of the control. If WordWrap is False, the line can extend past the edge of the text box and the user must press Enter to move to a new line.

Using text boxes effectively requires significant testing. Because of the free-entry functionality present in a text box, users may type incorrect data, which requires the programmer to provide validation to check what the user enters. VB.NET has new validation abilities. You can learn about the ErrorProvider control in the section "Provide Error Messages."

![](img/d6f772854306e15fb6df39b861a7b541_69_0.png)

- 1. Create a new Windows Application project or open an existing project.
- 2. Click and drag the Label control from the Toolbox to add it to the form.
- 3. In the Properties window, type a description of the text that users enter using the Text property.
  The text appears in the Label control on your form.
- 4. Click and drag the TextBox control in the Toolbox to add it to the form.
- 5. In the Properties window, remove the provided text by selecting the text and pressing the Delete key.
  If desired, type your own default value in the Text property.

## Apply It

In a multi-line TextBox control, the Lines property maintains an array of strings representing each line in the TextBox control. You can use this property to retrieve particular lines of information from the text box or to manipulate text in the control. The example below loads the contents of the property into a new array and displays each line in a ListBox control you must add to the form.

## TYPE THIS:

```vb
Public Sub GetTextBoxContents()
' Create a string array and store the contents of the Lines property.
Dim textLines() As String, line As String
textLines = TextBox1.Lines

For Each line In textLines
    ListBox1.Items.Add(line)
Next
End Sub
```

## RESULT:

This is line #1 in the text box.

This is line #2 in the text box.

![](img/d6f772854306e15fb6df39b861a7b541_70_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_70_1.png)

## CREATE A MULTI-LINE TEXT BOX

- 6. With the Text Box control selected, double-click the Multi-line property to toggle it to True in the Property window.
- 7. Click the ScrollBars property's arrow and select a constant for the scrollbar style you desire.
- 8. Press F5 to run your project.

The TextBox displays text and enables the user to edit the text in a standard way.
