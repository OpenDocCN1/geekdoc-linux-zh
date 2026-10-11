+   * The command q in vim Linux editor is used to exit the system if you have made no changes to buffer data.
+   * The command wq in vim Linux editor is used to save buffer data to file and then exit the editor.
+   * The command q! in vim Linux editor is used to quit the editor and then discard the changes that are made to the data of buffer.
+   * The command w filename in vim Linux editor is used to save your file with a different filename.

# ## Data Editing

When you are in the insert mode, you may insert data in the buffer. Sometimes you have to add or remove some data after entering into the buffer. While you are in normal mode, the vim editor will provide certain commands for editing data in the buffer. You should take extra care when you try to use a PC keyboard Delete or Backspace keys while you are inside the vim editor. The vim editor recognizes the keyboard Delete key as an x command functionality, which will delete a character at the current cursor location.

# ## Copy & Paste

A standard feature of these editors is their ability to make a cut or copy data, and after that, paste it into the document. Cutting and pasting text is easy. When vim removes your data, it will forward it into a separate register. You can then retrieve that data by using the p command. You can use the dd command to remove different lines of text. When you try to copy text, you may find it a bit trickier.

+   * x in vim Linux editor is used to delete a character at the cursor's current position.
+   * R text in vim Linux editor is used to overwrite the data at the cursor's current position with the text until you hit the Escape key.
+   * r char in vim Linux editor is used to replace any single character