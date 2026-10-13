FIGURE 18.12
The Permissions dialog box.

![](bbox=[0.3, 0.2, 0.62, 0.55])

All the permissions were covered in Hour 4, "Basic UNIX Shell Use," with the exception of the SetUID and SetGID ones. Basically, if these boxes are checked and this is a binary file that can be executed, it will be run as the user who owns the file no matter who actually runs the file. This also means that it will have all the permissions and access rights of the owner instead of the user who actually ran the file. Unless you fully understand the implications of doing this, you should leave these two options alone.

> SetUID and SetGID can be a serious security hole if used improperly because they can allow a user to run programs as another user. There are very few times when this is actually necessary, so you will almost never need to use these options in the Permission dialog box of KDE's file manager.

# Searching for Files

Inevitably, you will save a file and then not remember where you put it when you come back for it later. To help you find it, you can select Find Files from the K menu. This will bring up the window shown in Figure 18.13.

In the Named box, simply type in the name of the file that you are looking for. If you don't know the file's whole name, you can use wildcards. For example, my* will find all files beginning with my. By default, the program starts looking in your home directory and also checks all directories under your home directory. You can change the directory that the search starts at by clicking the Browse button. In addition, if you don't want to