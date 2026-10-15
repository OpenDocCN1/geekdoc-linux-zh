
## Apply It

You can create a simple text file printer using a combination of the PrintDocument and Stream commands. For this code to work, you need a Button named Button1 and a PrintDocument named PrintDoc.

### TYPE THIS:

```
Private printFont As New Font("Arial", 10), streamToPrint As IO.StreamReader

Private Sub Button1_Click(ByVal sender As Object, ByVal e As EventArgs)
    streamToPrint = New IO.StreamReader("C:\My Documents\MyFile.txt")
    PrintDoc.Print()
End Sub

Private Sub PrintDoc_PrintPage(ByVal sender As Object, ByVal e As _
System.Drawing.Printing.PrintPageEventArgs)
    Dim linesPerPage As Single = e.MarginBounds.Height / printFont.GetHeight(e.Graphics)
    Dim line As String = Nothing, count As Integer, yPos As Single = 0
    For count = 0 To linesPerPage - 1
        line = streamToPrint.ReadLine()      ' print each line of file.
        If line Is Nothing Then Exit For    ' no more lines in file
        yPos = e.MarginBounds.Top + count * printFont.GetHeight(e.Graphics)
        e.Graphics.DrawString(line, printFont, Brushes.Black, _
            e.MarginBounds.Left, yPos, New StringFormat())   ' output line of text
    Next
    If Not (line Is Nothing) Then e.HasMorePages = True    ' print another page?
End Sub
```

### RESULT:

The text file prints to the default printer.

![](img/d6f772854306e15fb6df39b861a7b541_138_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_138_1.png)

VB .NET creates the event handler.

8 Declare a variable to access the Graphics object.

9 Type code to draw onto the page.
Note: See Chapter 5 for information on graphics commands.

10 Type code to set HasMorePages.

11 Press F5 to run the project.

When the appropriate method or event runs, the pages generate and print to the printer.

## USING THE PRINTER DIALOG BOX

Before an application prints, it often presents a Printer selection dialog box to let the user select which printer to use and any printer driver options, such as draft mode. You can add the Print dialog box to your application using the PrintDialog control.

The PrintDialog control is available in the Windows Form section of the Toolbox. A required property for the function of the PrintDialog control is Document. You must set this property to a valid Document provided by a PrintDocument control.

Other than the Document property, you can edit properties to determine what functions to make available to the user. AllowPrintToFile enables or disables the "Print To File" checkbox. If AllowPrintToFile is True and the user checks the box, the PrintToFile property is set to True. AllowSelection enables or disables the range selector boxes, which enable the user to print only a particular range of pages. AllowSomePages enables or disables the box where the user can enter a selection of pages either individually or by range. If you enable these properties, the PrintDocument control manages the correct pages to print.

To make the dialog box appear, invoke the ShowDialog method with no arguments. The method returns a DialogResult specifying either OK or Cancel. For more information on DialogResult, see Chapter 3. If the user clicks OK, the PrinterDialog sets the dialog box settings to the PrinterSettings of the PrintDocument component. If you call the ShowDialog method and the user does not have any defined printers, a message appears notifying the user how to add a printer and the DialogResult returns Cancel. You can use the Reset method to clear any previous settings the user has made and reset the dialog box to defaults.

The example uses a Button control to activate the Print dialog box. You can use a variety of controls such as a toolbar or menu as well.

![](img/d6f772854306e15fb6df39b861a7b541_139_0.png)

- 1. Open a form in a Windows Application project.
- 2. Add and configure a PrintDocument component on the form.

> Note: See the section "Using the PrintDocument Control" to add a PrintDocument to the form.

- 3. In the Toolbox, double-click the PrintDialog control to add it to the form.
- The control appears in the Component Tray.

- 4. In the Properties window, click the Document and select PrintDocument control.
- You can optionally set other properties and toggle preference properties like AllowSelection by double-clicking the property name.

- 5. Open the method or event where the Printer dialog box needs to appear.
