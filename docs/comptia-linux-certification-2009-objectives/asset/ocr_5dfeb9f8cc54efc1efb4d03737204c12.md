# How to Locate Files

# Procedure Reference: Search for Files from the Database

To search for files from the database:

+   1. Log in as root.
2. Enter `updatedb` to update the mlocate database with the file name and path information.
3. Enter `locate {string}` to search the updated database for the specified string.

# Procedure Reference: Search for Files Using the GNOME Search Tool

To search for files using the GNOME search tool:

+   1. Log in as a user in the GUI.
2. Choose **Places**→**Search for Files** to open the search tool.
3. In the **Search for Files** window, in the **Name contains** text box, type the string to be searched.
4. If necessary, from the **Look in folder** drop-down menu, choose the location to perform the search.
5. If necessary, click the toggle button beside the text “Select more options” to specify additional search criteria such as **Date modified less than**, **Date modified more than**, **Size at least**, **Size at most**, **File is empty**, **Owned by user**, **Owned by group**, **Owner is unrecognized**, **Name does not contain**, **Name matches regular expression**, **Show hidden and backup files**, **Follow symbolic links**, and **Include other filesystems**. Click **Add** to add the selected option.
6. If necessary, click **Help** to view the manual on “Search for Files.”
7. Click **Find** to search for the specified string.