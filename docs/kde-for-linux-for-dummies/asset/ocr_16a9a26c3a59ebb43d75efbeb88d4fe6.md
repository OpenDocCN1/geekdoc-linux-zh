+   2. **Type a program name in the Open With text box.**
+      Enter the name of the program you want to use to open the selected file. Be sure to use the name of the executable file, not the name as it appears on a menu somewhere. For example, type `kview` to use the KDE Image Viewer utility.

+   3. **Click OK.**
+      KFM launches the program, which then loads the selected file.

![](bbox=[0.13, 0.27, 0.23, 0.36])

To automatically open a document file in its parent program, click the document file in a KFM window. If KFM can identify the file type and its associated program, KFM launches the program and passes the file name to the program, so the program automatically loads the selected file.

If you want KFM to automatically launch the correct program when you click a document file, KFM must be able to identify the file type, and it must know what program to launch to open that file type.

A standard set of file type descriptions (called *MIME types*) and a set of default links between certain file types and some of the standard KDE utility programs, are both parts of the normal KDE installation. As a result, KFM starts out with a respectable number of file types that you can open with a single click. In addition, when you install new KDE programs, the installation routine should set up MIME types for the program's file types — and add links between those file types and the program so you can automatically open those files in the newly installed program.

Sometimes, you may need to create or customize the association between document file types and the application used to open them. You'll probably never need to create an actual MIME type from scratch; you probably won't even need to edit any existing MIME types. (So you're off the hook; this book won't drag you through creating MIME types.) If you want to use a specific program to open a particular kind of file, you may need to change the established links between the file type and the program KFM uses to open those files. You revise the application links by following these steps:

+   1. **Open a KFM window and choose Edit Applications.**
+      KFM displays the contents of a hidden subdirectory of your home directory, `~/.kde/share/appLink`. This directory contains a series of link files and folders that correspond to the contents of the KDE menu.

+   2. **Navigate the subfolders to locate the application you want to change.**
+      Open folders and subfolders as needed until KFM displays the icon for the link to the application you want to use to open the target file type.