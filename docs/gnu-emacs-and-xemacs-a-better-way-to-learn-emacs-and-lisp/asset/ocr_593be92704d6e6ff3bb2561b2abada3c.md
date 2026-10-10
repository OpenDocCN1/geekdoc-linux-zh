This command makes the keybinding `Ctrl-c m` work in all modes. Chapter 10 will show you how to make a keybinding active in just a single mode.

# Macros That Query

Two types of macros stop and ask for input at specified times, similar to the query-replacement commands discussed in Chapter 3. The first incorporates the recursive-editing facility that is also used within a query-replace operation.

Recursive editing in a macro is useful when you're creating fill-in-the-blank forms. Stepping through a simple example is probably the easiest way to show you how this is done.

+   1. Start the macro by pressing `Ctrl-x (`.
+   2. The first item in the form is a person's name, immediately followed by the command that begins a recursive edit. Type `Name:` and press `Ctrl-u Ctrl-x q`.
+   3. Square brackets appear on the mode line when you are in the midst of a recursive edit. When the macro is being executed (after it is recorded), this is when you type in a name. Press `M-Ctrl-c` to exit the recursive edit.
+   4. This takes you back to macro recording. Now you type in the next field of the form, followed again by the recursive-edit command. Type `Address:` and press `Ctrl-u Ctrl-x q`.
+   5. Again, you leave recursive editing to type in a third field. Press `M-Ctrl-c`, type `Date of Birth,`, and press `Ctrl-u Ctrl-x q`. Then re-enter recursive editing by pressing `M-Ctrl-c`.
+   6. End the macro now (even though you can define any number of fields) by pressing `Ctrl-x )`. You've just created an interactive template for writing a form. When you execute this type of macro, you have to execute the exit-recursive-edit command (`M-Ctrl-c`) after filling out each of the form's fields.

The second type of query macro doesn't use recursive editing. It instead stops at predefined points during the macro's execution to ask you what you want to do next.

Here is an example showing how this variant works. The purpose of this macro is to search a file for lines beginning with “Note” and then copy the first sentence and paste it into a new file called notes.txt. The reason for the query is to let you decide if you want each sentence copied or not.

+   1. Press `Ctrl-x (` to start recording the macro.
+   2. Do a regexp search for `Notes,`, but only at the beginning of a line.
+   Press `M-Ctrl-s` and type `^Note.`, (Remember that the caret (^) signifies that the match must be at the beginning of a line.)