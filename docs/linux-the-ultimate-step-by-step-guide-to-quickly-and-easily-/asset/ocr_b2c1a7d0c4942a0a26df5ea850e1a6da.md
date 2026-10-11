```
Hello there.
```

Here is some text.

# To save type:

```
CTRL-O
```

This is the letter “o,” not a zero. It will ask you to confirm the name of the file you wish to save to:

```
File Name to Write: file1
```

+   - ^G Get Help M-D DOS Format M-A Append
+   - M-B Backup File

```
^C Cancel M-M Mac Format M-P Prepend
```

As you can see, the options at the bottom have also changed. These are contextual, meaning they will change depending on what you are trying to do. If file1 is still the file you wish to write to, hit “ENTER.”

If we make additional changes and wish to save the file and exit the program, we will see a similar prompt. Add a new line, and then try to exit the program by typing:

```
CTRL-X
```

If you have not saved after making your modification, you will be asked whether you wish to save the modifications you made:

```
Save modified buffer (ANSWERING "No" WILL DESTROY CHANGES) ?
Y Yes N No ^C Cancel
```

You can type “Y” to save your changes, “N” to discard your changes and exit, or “CTRL-C” to cancel the exit operation. If you choose to save, you will be given the same file prompt that you received before, confirming that you want to save the changes to the same file. Press ENTER to save the file and exit the editor.

You can see the contents of the file you created using either the cat command to display the contents, or the less command to open the file for viewing. After viewing with less, remember that you should hit q to get back to the terminal.

```
less file1
Hello there.
```