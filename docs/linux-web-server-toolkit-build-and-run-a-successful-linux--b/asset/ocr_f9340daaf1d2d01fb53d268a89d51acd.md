# 264 Linux Web Server Toolkit

![](bbox=[0.173, 0.083, 0.703, 0.287])

Figure 10-8: This shows a second example of a selection list, with MULTIPLE selection enabled and a scroll bar used because the SIZE parameter of the <SELECT> tag is greater than 1.

# TEXT AREAS

Although you use the <INPUT> tag with a TYPE=TEXT to let a user enter a line of text, this tag always displays a single-input field. In many instances, you will want the user to enter a longer block of text, such as a comment or description. The <textarea> tag allows you to do this, specifying the size of the text box that will appear in the browser.

The <textarea> tag is also different from other form tags because it has a closing tag. The options for the interface element are in the <textarea> opening tag, but all the text between the opening tag and the </textarea> closing tag is displayed as the default text in the text box. This can be used to include a line like "Enter your comment here". It can also be left blank but then filled in automatically by a script that generates a form, so that it contains some longer passage of text for the user to review or edit.

The parameters allowed with the <textarea> tag are NAME (required), ROWS (how high the box should be, measured in lines), and COLS (how wide the box should be, measured in characters). The default values used if you don't include ROWS and COLS depend on the user's browser. But even if you don't specify a size, the <textarea> is intended for larger blocks of text and will include scroll bars as needed.

The following example of a <textarea> tag is displayed in a browser Figure 10-9.

```
<textarea NAME=COMMENTS ROWS=10 COLS=40>
Enter your comments here
</textarea>
```