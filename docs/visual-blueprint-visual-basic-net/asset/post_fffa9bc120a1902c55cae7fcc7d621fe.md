
## Using the Rich Text Control

You can use the RichTextBox to enter rich data, such as formatted text, pictures, and OLE objects. An example of the rich text box in use is WordPad, a program included with Windows. You can create much of the functionality available in WordPad in your application.

The RichTextBox control stores the data inside the box in RTF format. Most applications can understand this format, so you can cut and paste rich text to and from applications such as Microsoft Word into this control during runtime. Similarly to the TextBox control, you can use the Text property to read or set the plain text of the box. The Rtf property returns the text with all of the formatting codes. When you set the AcceptsTab property to True, the user can enter a tab as text into a control. If the property is False, the focus shifts to the next control.

Scroll bars only show if the user types more than can fit in the box's boundaries. The ScrollBars property allows you to set the control to None, Vertical, Horizontal, or Both scrollbars. The other settings for the property are FixedHorizontal, FixedVertical, and FixedBoth; they force the specified scrollbars to show.

Runtime properties play an important role in using the RichTextBox control's abilities. Formatting properties work for the selected text. Use the SelectionStart and SelectionLength properties to choose the starting point, and the length of the selection, respectively. If the user makes a selection, these properties update automatically. The first character in the box is index zero for the RichTextBox control.

You can use the SelectedText and SelectedRtf properties to receive or set the text enclosed in the selection. You can also use the selection to change the format of the selected text. For example, the SelectionBullet property adds bullets to the selected lines of the control when set to True.

![](img/d6f772854306e15fb6df39b861a7b541_71_0.png)

- 1. Create a new Windows Application project or open an existing one.
- 2. From the Toolbox, click and drag the RichTextBox control onto the form to the size you desire.
- 3. Add a control for the user to alter the formatting of the rich text.
- 4. Double-click the control to alter the formatting.

### Apply It

After the user specifies a selection, or you set a selection code, you can format the text by reassigning the text's SelectionFont to a new Font class. SelectionColor allows you to reassign a color to the selected text. Set SelectionBullet = True to make the selected lines into bulleted items.

The SelectionIndent, SelectionRightIndent, and SelectionHangingIndent affect the paragraphs that have selected text inside them. These properties allow you to specify a pixel amount for the various indentation styles.

### Type This:

```vb
Private Sub Button1_Click(ByVal sender As System.Object, _
ByVal e As System.EventArgs) Handles Button1.Click
    ' Store the font for the selected text.
    Dim tempFont As System.Drawing.Font = RichTextBox1.SelectionFont
    ' Create FontStyle to contain the style for the current selection.
    Dim tempStyle As System.Drawing.FontStyle = RichTextBox1.SelectionFont.Style
    ' Determine whether the current text selection is bold.
    If tempFont.Bold = True Then
        ' Create a new font based on the existing font for selection,
        ' but use an exclusive or bitwise operator to remove the bold style.
        RichTextBox1.SelectionFont = New Font(tempFont.FontFamily, _
        tempFont.Size, tempStyle And Not FontStyle.Bold)
    Else
        ' Create a new font based on the existing font for selection,
        ' but use an exclusive or bitwise operator to remove the bold style.
        RichTextBox1.SelectionFont = New Font(tempFont.FontFamily, _
        tempFont.Size, tempStyle Or FontStyle.Bold)
    End If
End Sub
```

### Result:

Font switches between bold and normal styles.

![](img/d6f772854306e15fb6df39b861a7b541_72_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_72_1.png)

The default event for the control loads in the code editor.

In this example, the selected text toggles between bold and standard text.

The rich text box allows editing.

You can see formatting changes by completing the necessary action to run the event or method code.

- 5. Type the appropriate code to alter the selection.
- 6. Run the project by pressing F5.
