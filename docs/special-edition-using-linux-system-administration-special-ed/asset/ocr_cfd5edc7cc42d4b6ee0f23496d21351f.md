+   - `retain`—Adds the list of header fields named to the retained list. Only the header fields in the retain list are shown on your terminal when you print a message. All other header fields are suppressed. The Type and Print commands can be used to print a message in its entirety. If retain is executed with no arguments, it lists the current set of retained fields.
+   - `save`—(s) Takes a message list and a filename and appends each message in turn to the end of the file. The filename in quotes, followed by the line count and character count is echoed on the user’s terminal.
+   - `set`—(se) With no arguments, prints all variable values. Otherwise, sets option. Arguments are of the form `option=value` (no space before or after `=`) or option. Quotation marks can be placed around any part of the assignment statement to quote blanks or tabs, for example, “set indentprefix=.”.
+   - `saveignore`—saveignore is to save what ignore is to print and type. Header fields thus marked are filtered out when saving a message by save or when automatically saving to mbox.
+   - `saveretain`—saveretain is to save what retain is to print and type. Header fields thus marked are the only ones saved with a message when saving by save or when automatically saving to mbox. Saveretain overrides saveignore.
+   - `shell`—(sh) Invokes an interactive version of the shell.
+   - `size`—Takes a message list and prints out the size in characters of each message.
+   - `source`—The source command reads commands from a file.
+   - `top`—Takes a message list and prints the top few lines of each. The number of lines printed is controlled by the variable toplines and defaults to five.
+   - `type`—(t) A synonym for print.
+   - `unalias`—Takes a list of names defined by alias commands and discards the remembered groups of users. The group names no longer have any significance.
+   - `undelete`—(u) Takes a message list and marks each message as not being deleted.
+   - `unread`—(u) Takes a message list and marks each message as not having been read.
+   - `unset`—Takes a list of option names and discards their remembered values; the inverse of set.
+   - `Visual`—(v) Takes a message list and invokes the display editor on each message.
+   - `write`—(w) Similar to save except that only the message body (without the header) is saved. Extremely useful for such tasks as sending and receiving source program text over the message system.
+   - `xit`—(x) A synonym for exit.
+   - `z`—mail presents message headers in windows as described under the headers command. You can move mail’s attention forward to the next window with the z command. Also, you can move to the previous window by using z.