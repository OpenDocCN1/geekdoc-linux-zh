# ## ACTIVITY 9-1

# Using Wildcards to Search for Files

**Data Files:**

+   Audit_File_2000.txt, Audit_File_2001.txt, Audit_File_2002.txt, Audit_File_2003.txt, Audit_File_2004.txt, Audit_File_2005.txt, Audit_File_2006.txt, Audit_File_2007.txt, Audit_File_2008.txt, Audit_File_2009.txt

**Before You Begin:**

+   1. You have logged in as root in the GUI and CLI.

+   2. The terminal window is displayed.

+   3. On the terminal window, enter

+   cp /085039Data/Working_with_Bash_and_Shell_scripts/* /root.

+   4. Enter *y* to continue.

+   5. Enter `cd /root`.

+   6. Enter `clear` to clear the terminal window.

+   7. Switch to the CLI.

+   8. Log in to the system as root.

**Scenario:**

You have to create a report on audit file maintenance in your department. You want to generate a list of all the audit files created since the inception of the company, along with the date and time of creation, ownership details, and file access permissions. Therefore, you decide to use wildcards to search for the audit files in your Linux system.

| What You Do | How You Do It |
|---|---|
| 1. Search for the audit files using wildcards. | a. Enter `ls -l Audit*` to list all files that match the search pattern.<br>b. Observe that the resultant files are displayed along with the date and time of creation, ownership details, and file permissions. |
| 2. Display all file names using wildcards. | a. Enter `echo Audit*` to display all file names that match the search pattern.<br>b. Observe the file names that are displayed.<br>c. Clear the terminal screen. |