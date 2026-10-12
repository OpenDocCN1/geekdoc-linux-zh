# Beginner's guide to nano

![](bbox=[0.24, 0.11, 0.66, 0.24])

# Save and exit

**04** Once you've finished modifying the file and need to get on with the next task, you can press Ctrl+X to exit nano. It will ask if you want to save any modifications, which just requires a Y to confirm. If you want to exit without saving changes, you can just use N. To cancel before making a decision, use Ctrl+C.

# Advanced navigation

**07** You've probably been using space as the arrow keys to move one space at a time left, right, up or down. There are other ways to move around the file, though. Using Ctrl+A will act the same way as the Home key does in a graphical editor, moving the cursor to the start of the line. Same with Ctrl+E moving you to the end line. The End key. Ctrl+V is page down, and Ctrl+Y is page up.

![](bbox=[0.03, 0.47, 0.22, 0.59])

# Save and continue

**02** Once you've finished with nano you can save/write out using Ctrl+O. All shortcuts and functions such as this are done using Ctrl and a letter key. It will ask you what name to save the file under. Whatever you name it, it will be saved in the directory you opened nano from unless you specify a path.

# Searching a file

**08** Sometimes you'll be looking for a specific line or phrase in a large text file. Instead of using the arrow keys and tirelessly reading every line, you can use the search function with Ctrl+W. Enter the search term will bring up a box in the nano document, and once you've finished you can press Ctrl+C to exit the search.

![](bbox=[0.32, 0.46, 0.51, 0.59])

# Copy and paste

**05** This is more of a terminal-specific command, but it can be unusual as well in nano. While you *can't* use the mouse to navigate around the file in nano, you can highlight text in the same way you would in a graphical text editor. Once highlighted, pressing Ctrl+Shift+C will copy any text. Ctrl+Shift+V will paste.

![](bbox=[0.03, 0.82, 0.22, 0.95])

# Opening files

**03** To edit already existing files, you'll first need to know their location and name. To open them in nano, type the following:
$ nano /path/filename
For example, to edit /fstab you would type:
$ nano /etc/fstab

![](bbox=[0.67, 0.66, 0.85, 0.8])

# Extra help

**09** There are many more functions available in nano than this list. Get a full list of commands with this what they do. The caret symbol (^) in this list denotes the use of Ctrl on your keyboard.

![](bbox=[0.32, 0.82, 0.51, 0.95])

# Insert from file

**06** If you need to directly insert the contents of another file, there's a quick way to do it without needing to use copy and paste. Typing Ctrl+R and entering the path to the file will insert it into the spot your cursor is at.