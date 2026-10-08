+   1. **Bring up the Icon Editor** from the Desktop\_Apps (HP-UX), Desktoptools (AIX), or from the Desktop\_Tools, on Solaris all in the Application Manager.

+   2. Choose **File -> Open**.

+   3. Enter a path or folder name: **/opt/dynatext/data/bitmaps**.

+   4. Enter the file name: **logoicon.bm**

+   5. Choose **Open**.

We’ll see the icon and that it is indeed 32x32. Now we need to save the icon to our own .dt directory.

+   6. Choose **File -> Save As**.

+   7. Enter path or folder name: **/$HOME/.dt/icons**. For the adminl user, that would be in **/home/admin1/.dt/icons**.

If we were going to do this task globally, we’d put this in **/etc/dt/appeconfig/types/C**.

+   8. Leave the file name as is.

+   9. **Save**.

Now that we have the icon, we need to create an action file and a description file to go with it.

+   1. **Using your favorite Text Editor**, enter the following:

```
ACTION instinfo
{
    LABEL       instinfo
    TYPE        COMMAND
```