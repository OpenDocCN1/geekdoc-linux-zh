ways to end the work session in Linux, depending on whether we are in graphic mode or text.

In-text mode:

+   1. Press the <ctrl> d keys
+   2. Enter the exit command.

In graphic mode:
The output of X Window depends on the window manager that is running and will be explained later.

# Linux File System Structure

Files: Types

The basis of the Linux filing system will include the file, which is nothing other than the structure used by the operating system to store information on a physical device such as a hard drive, a floppy disk, a CD-ROM or a DVD. Naturally, a file can contain any type of information that you would ilke, from an image in PNG or JPEG format to a text or a web page in HTML format. The file system is the structure that allows Linux to handle the files it contains.

All Linux files have a name, which must comply with certain rules:

+   * A file name can be between 1 and 255 characters
+   * You can use any character except the slash / and it is not recommended to use the characters with special meaning in Linux, which are the following: = \ ^ ~ "* *; -? [] ! & ~ <>  
+   	* To use files with these characters or spaces you must enter the name of the file between quotation marks
+   * Numbers can also be used if desired.
+   * Uppercase and lowercase letters are considered different, and therefore letter.txt is not the same as Letter.txt or letter.Txt