# Output

![](bbox=[0.12, 0.17, 0.88, 0.58])

All the action takes place in the `while` loop. The `switch` statement processes keyboard input, calling the appropriate routine. Valid input consists of one of the following:

+   - F2—Add a record
+   - F3—Delete a record
+   - F4—Find a record
+   - F5—Get a record
+   - F6—List all records
+   - F10—Quit the program

Any other keystroke, when looking at this screen, causes the message `Key not defined` to be displayed in the status area. The success or failure of each operation is displayed on the status line using the `status` function. You can easily extend the program to accept other keystrokes as aliases for the currently defined commands. For example, typing `a` or `A` would allow the user to add a record, and typing `l` or `L` would list all records currently in the database.

When you press F2, you are first asked to enter the musician's name and then the CD title. The appearance of the screen after completing an add operation is shown in Figure 22.2.

If the key already exists in the database, an error message to that effect is displayed in the database.