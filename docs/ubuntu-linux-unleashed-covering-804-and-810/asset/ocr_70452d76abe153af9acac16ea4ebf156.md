The vi command works by using an insert (or editing) mode, and a viewing (or command) mode.

When you first start editing, you are in the viewing mode. You can use your cursor or other navigation keys (as shown later) to scroll through the text. To start editing, press the i key to insert text or the a key to append text. When finished, use the Esc key to toggle out of the insert or append modes and into the viewing (or command) mode. To enter a command, type a colon (:), followed by the command, such as w to write the file, and press Enter.

Although vi supports many complex editing operations and numerous commands, you can accomplish work by using a few basic commands. These basic vi commands are

+   - Cursor movement—h, j, k, l (left, down, up, and right)
+   - Delete character—x
+   - Delete line—dd
+   - Mode toggle—Esc, Insert (or i)
+   - Quit—:q
+   - Quit without saving—:q!
+   - Run a shell command—:sh (use 'exit' to return)
+   - Save file—:w
+   - Text search—/

# NOTE

Use the vintutor command to quickly learn how to use vi's keyboard commands. The tutorial takes less than 30 minutes, and it teaches new users how to start or stop the editor, navigate files, insert and delete text, and perform search, replace, and insert operations.

# Working with emacs

Richard M. Stallman's GNU emacs editor, like vi, is included with Ubuntu and nearly every other Linux distribution. Unlike other Unix and Linux text editors, emacs is much more than a simple text editor—it is an editing environment and can be used to compile