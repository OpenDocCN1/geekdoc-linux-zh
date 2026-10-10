+   - **emacs**. Originally written by Richard Stallman at MIT, **emacs** is a powerful, feature-rich editor known for its flexibility: **emacs** can be personalized to fit the personal tastes of the user. Some versions of **emacs** supported windowing before windowing systems became common on UNIX.

+   - **pico**. This editor is thought by many to be the easiest to use of the widely available UNIX editors. The menu structure of **pico** makes it especially friendly to the beginner.

+   - **xedit**. This X client is a simple window-based text editor. It is available on most systems that run X.

Because *vi* is likely to be found on nearly all UNIX systems, it is the editor featured in this book.

# ### 10.3 How a Text Editor Works

Regardless of the text editor you choose, the process of editing a text file can be summarized like this:

+   1. You start the editor and give it the name of a file to edit.

+   2. If you specified an existing file, the editor makes a copy of it and places the copy in a temporary workspace called the work buffer. If you are creating a new file, the editor simply opens up an empty work buffer.

+   3. You use editor commands to add, delete, and/or change the text in the work buffer. When you are satisfied with the changes you have made, you tell the editor to \"write into the file.\""

+   4. The editor saves the contents of the work buffer in the file. If you are editing an existing file, the editor replaces the original file with the updated version in the buffer.

Note that you do not work directly on the file, but only on the copy that is in the buffer. This means that if you leave the editor without writing your changes into the file, the changes are lost, and the original file is not altered.

# ### 10.4 Line and Screen Editors

All editors do much the same thing, but some are decidedly easier to use than others. The original UNIX editor *ed* is called a *line editor*, because it makes changes in the buffer line by line. To make a change using a line editor, you must first specify the line where you want the change to be made, and then you must specify the