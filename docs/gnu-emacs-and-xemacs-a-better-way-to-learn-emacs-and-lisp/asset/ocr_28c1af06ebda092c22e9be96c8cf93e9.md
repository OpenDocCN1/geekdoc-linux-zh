+   3. Pressing `Enter` stops the search. This is where the query takes place, letting you decide whether to accept the first match.
+   4. Press `Ctrl-x q. At this point, the macro is paused, waiting for a response. Pressing the spacebar or y signals Emacs that you want the macro to continue. Pressing `Delete` or n means you want to ignore this match and continue to the next one. Pressing `Enter` or Q means you want to quit the macro altogether.
+   5. Assuming that you pressed `y` or `n` (allowing the macro to continue), press `Ctrl-space` to set the mark.
+   6. Press `Ctrl-e` to move point to the end of the line.
+   7. Press `M-w` to copy the line to the kill ring.
+   8. Press `Ctrl-x Ctrl-f` and type `notes.txt` to create a new file called `notes.txt` in the current directory.
+   9. Press `Ctrl-y` to paste the copied line.
+   10. Press `Enter` to start a new line.
+   11. Press `Ctrl-x b` to go back to the original file.
+   12. Press `Ctrl-x )` to end the macro.

# ## Conclusion

Many Emacs users find that the configurability provided by Customize and key-board macros is all they need.

As useful as these tools are, you might eventually need to accomplish something in Emacs that is outside their scope. The next chapter introduces you to the Emacs-Lisp language, which makes this possible.