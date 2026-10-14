The uppercase U command undoes all changes to the current line and restores the line to its original state. The U command works only if you have not moved the cursor to another line.

# A.1.8 Finishing Your Edit Session

After you finish the exercises in this appendix, you should save the file and quit vi. To save your changes and quit vi, enter:

```
:wq Return
```

If you want to quit vi without saving your changes, you can do so by entering:

```
:q! Return
```

You have now learned enough about vi to edit any file. The following sections show you some advanced techniques that can improve your productivity and let you customize your environment.

# A.2 Using Advanced Techniques

This section shows you how to search for text strings, move text, and copy and paste text. As you work with larger documents, all these tasks increase your ability to work efficiently.

# A.2.1 Searching for Strings

In a large document, searching for a particular text string can be very time consuming. The slash (/) command is used to search for a string. When you enter the slash (/), you are prompted for a text string as the target of the search. When you press the Return key, vi searches the file for the first occurrence of the text string you entered.

If you do not have it open, reopen the my.file file. Move to the top of the document using one of the cursor movement keys you learned earlier in this appendix. To search for the text string th, enter the following:

```
/th Return
```

As soon as you enter the slash (/) command, the slash (/) is displayed at the bottom of the screen (similar to the way in which the colon (:) works). When you entered the text string th, it was echoed (displayed) at the bottom of the screen. You can use the Backspace key to fix mistakes when you enter the search string.

After you press the Return key, the cursor moves to the first occurrence of the string (the th in the word this). The n (next) command continues the search for the next occurrence of the last string you searched for. Try it now by entering: