# USING THE RICH TEXT CONTROL

You can use the RichTextBox to enter rich data, such as formatted text, pictures, and OLE objects. An example of the rich text box in use is WordPad, a program included with Windows. You can create much of the functionality available in WordPad in your application.

The RichTextBox control stores the data inside the box in RTF format. Most applications can understand this format, so you can cut and paste rich text to and from applications such as Microsoft Word into this control during runtime. Similarly to the TextBox control, you can use the Text property to read or set the plain text of the box. The Rtf property returns the text with all of the formatting codes. When you set the AcceptsTab property to True, the user can enter a tab as text into a control. If the property is False, the focus shifts to the next control.

Scroll bars only show if the user types more than can fit in the boxes boundaries. The ScrollBars property allows you to set the control to None, Vertical, Horizontal, or

Both scrollbars. The other settings for the property are FixedHorizontal, FixedVertical, and FixedBoth; they force the specified scrollbars to show.

Runtime properties play an important role in using the RichTextBox control's abilities. Formatting properties work for the selected text. Use the SelectionStart and SelectionLength properties to choose the starting point, and the length of the selection, respectively. If the user makes a selection, these properties update automatically. The first character in the box is index one for the RichTextBox control.

You can use the SelectedText and SelectedRtf properties to receive or set the text enclosed in the selection. You can also use the selection to change the format of the selected text. For example, the SelectionBullet property adds bullets to the selected lines of the control when set to True.

![](bbox=[0.05, 0.62, 0.95, 0.88])

+   1. Create a new Windows Application project or open an existing one.
+   2. From the Toolbox, click and drag the RichTextBox control onto the form to the size you desire.
+   3. Add a control for the user to alter the formatting of the rich text.
+   4. Double-click the control to alter the formatting.