# **ACTIVITY 4-4**

# **Searching for Files in the GUI**

**Before You Begin:**

+   1. You have logged in as **root** in the CLI.
2. On the terminal, enter `chown -R jsmith /085039Data/Locating_Files/*` to change the ownership.
3. Enter `mkdir /work_files` to create `work_files` directory.
4. Enter `cp -pR /085039Data/Locating_Files/* /work_files` to copy the files.
5. Enter `clear` to clear the terminal screen.

**Scenario:**

As a system administrator, it is your responsibility to perform a regular system cleanup. You want to clear all the unnecessary empty files. You decide to search for empty files on the Linux filesystem to mark them for deletion.

| What You Do | How You Do It |
| :--- | :--- |
| 1. Open the GNOME search tool. | a. Switch to the GUI. <br> b. Log in as **root**. <br> c. Choose **Places→Search for Files** to open the GNOME search tool. |
| 2. Specify the search location as the `/work_files` directory. | a. In the **Search for Files** window, in the **Name contains** text box, type `*` to include all files for the search. <br> b. From the **Look in folder** drop-down menu, select **Other** to open the **Browse** window. <br> c. In the **Places** list box, double-click **File System** to display more destination directories in the right pane. <br> d. In the **Browse** window, in the **Name** list box, scroll down to view more directories. <br> e. In the **Name** list box, select **work_files** and click **Open** to select the `/work_files` directory and exit the window. |

Note: This table spans multiple sections on the page. Row 1 ends at y-0.59. Row 2 continues to y-0.89.