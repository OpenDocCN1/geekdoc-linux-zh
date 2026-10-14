3. Now type the text to expand it to:
`Global expansion for "ww": Walla Walla, Washington RET`

Now, whenever you type the text "ww" followed by a whitespace or punctuation character in the current buffer, that text will expand to the text "Walla Walla, Washington."

To save the abbrevs you have defined so that you can use them later, use the `write-abbrev-file` function. This saves all of the abbrevs currently defined to a file that you can read in a future Emacs session. (You can also open the file in a buffer and edit the abbrevs if you like.)

⇒ To save the abbrevs you have currently defined to the file "~/.abbrevs, type:
`ALT-X write-abbrev-file RET ~/.abbrevs RET`

Then, in a future Emacs session, you can use the `read-abbrev-file` function to define those abbrevs for that session.

⇒ To read the abbrevs from the file "~/.abbrevs, and define them for the current session, type:
`ALT-X read-abbrev-file RET ~/.abbrevs RET`

**NOTES:** Emacs mode commands are toggles. So to turn off `abbrev-mode` in a buffer, just type `ALT-X abbrev-mode RET` again. If you turn `abbrev-mode` on in that buffer later on during the Emacs session, the abbrevs will be remembered and will expand again.

# 10.1.6 Recording and Running Macros in Emacs

A *macro* is like a recording of a sequence of keystrokes—when you run a macro, Emacs executes that key sequence as if you had typed it.

To begin recording a macro, type `CTRL-X (` . Then, everything you type is recorded as the macro until you stop recording by typing `CTRL-X )` . After you have recorded a macro, you can play it back at any time during the Emacs session by typing `CTRL-X e` . You can precede it with the `universal-argument` command, `CTRL-U` , to specify a number of times to play it back.

⇒ Here are some ways to use this.

+   - To record a macro that capitalizes the first word of the current line (`ALT-C` capitalizes the word to the right of point) and then advances to the next line, type:
+     `CTRL-X ( CTRL-A ALT-C`
+     `CTRL-N CTRL-X )`