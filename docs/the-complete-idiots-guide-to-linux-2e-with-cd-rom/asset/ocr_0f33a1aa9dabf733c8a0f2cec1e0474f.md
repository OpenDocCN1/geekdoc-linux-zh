To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

# File Naming

You can name a file nearly anything you like. However, there are a few restrictions you’ll need to observe.

The new filename cannot be in use by another file in the same directory. If this is the case, the existing file will be replaced with the new file.

Filenames are case sensitive; in other words, Linux considers introduction.txt and Introduction.txt to be different files.

Certain characters—such as the asterisk (*), question mark (?), ampersand (&), vertical bar (|), circumflex (^), double quote (") , and apostrophe (')—should never be used, as these characters are special to the shell.

Characters such as the dash (-) and spaces should not be used because they will be hard to work with and delete when using a shell. The dash is used to specify program arguments. Some tools will not run properly when the name of a file begins with a dash, as the tools will behave as though you are specifying arguments instead of a filename. The space will make the shell think that you are specifying two different files (surround such names with quotes to access them from a shell). You should avoid these characters even if you only intend to work through KDE or another graphical environment.

Filenames will typically have an extension that indicates what type the file is. This extension is important because it tells KFM what application to use when opening the file by clicking on it.

Some common file types follow: