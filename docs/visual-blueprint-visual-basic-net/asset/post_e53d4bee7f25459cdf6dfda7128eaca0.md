
## Provide Input and Output

### Apply It

You can enable your users to select multiple files to open with OpenFileDialog when you set the MultiSelect property to True. When the dialog closes, the FileName property normally contains the file the user selected. For multiple selections, the FileNames array fills with the selected files.

### Type This:

```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click

    ' declare a variable to hold the result
    Dim result As DialogResult
    result = OpenFileDialog1.ShowDialog()
    ' only process the file list if the user hit the OK button
    If result = DialogResult.OK Then
        ' use a For Each loop to move through the array
        Dim fileName As String
        For Each fileName In OpenFileDialog1.FileNames
            ListBox1.Items.Add(fileName)
        Next
    End If
End Sub
```

### Result:

- C:\My Documents\Sample1.txt
- C:\My Documents\Sample2.doc
- C:\My Documents\Sample3.xls

![](img/d6f772854306e15fb6df39b861a7b541_136_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_136_1.png)

5. In the method or event where the dialog box needs to appear, declare a variable to hold the dialog box result.

6. Type `result = OpenFileDialog1.ShowDialog()`, replacing `result` with the variable name, and `OpenFileDialog1` with the name of the control.

7. Type code to respond to the dialog box.

8. Press F5 to run the project.

The file dialog box appears and allows file selection.

## Using the PrintDocument Control

Users expect solid printing abilities in any application. The computer monitor does not provide the resolution to make reading completely comfortable. You can use the PrintDocument control to provide the foundation of a printing system in your Windows Forms application.

VB.NET integrates all printing facilities into a combined system that works together. A PrintDocument provides you with a surface to draw contents onto the pages of your document. The PrintDocument control appears in the Toolbox under Windows Forms.

To begin printing the document, you call the object's Print method. Because of the integration, a variety of dialog boxes work with the PrintDocument control. See the section "Using the Printer Dialog" to provide a PrintDialog control to present printer options to the user. A Page Setup dialog box lets the user set up margins and page sizes; for details, see the section "Using the Page Setup Dialog."

When it receives a print command, the PrintDocument fires the BeginPrint event. This lets you perform initialization. For more information on events, see Chapter 2. After BeginPrint completes, the PrintPage event fires. You then draw the page onto the Graphics object provided by the event argument `e`. For more information on graphics, see Chapter 6. The event's argument also provides a MarginBounds rectangle, which gives you the prescribed boundaries to print within. The `e.PageSettings` provides a list of all the settings the PrintDocument uses to process the print job.

When you finish drawing a page, you must determine if your application needs to print another page. Set `e.HasMorePages` equal to True if you need to print another page and False otherwise. If you set `HasMorePages` to True, the event fires again. The current number of the page that the event expects you to print is not available. You need to use module level variables to store information about previously printed pages.

### Using the PrintDocument Control

![](img/d6f772854306e15fb6df39b861a7b541_137_0.png)

1. In a form of a Windows Application project, double-click the PrintDocument control in the Toolbox.

2. In the Properties window, type a name for the document in the DocumentName property.

3. Double-click the control you want the user to press to begin printing.

4. Type `PrintDocument1.Print()`, replacing `PrintDocument1` with the name of the control.

5. In the module level, declare necessary storage variables.

6. Click the PrintDocument control from the component list.

7. Click the PrintPage event from the event list.

The default event of the control appears in the Code Editor.
