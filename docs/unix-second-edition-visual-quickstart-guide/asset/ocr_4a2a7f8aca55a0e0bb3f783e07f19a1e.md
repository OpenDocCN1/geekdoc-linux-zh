# 2. ls -l file*

Optionally, verify that the file was created by typing ls -l file*. As shown in Code Listing 2.2, you’ll see the name of the new file as well as its length (0) and the date and time of its creation (likely seconds before the current time, if you’re following along).

# ✓ Tips

+   - You can also use touch to update a file’s date and time. For example, typing touch -t 12312359 oldfile at the prompt would update oldfile with a date of December 31, 23 hours, and 59 minutes in the current year. Or, typing touch -t 200312312359 new_years.eve would update the file called new_years.eve to the same time in the year 2003.

+   - Each time you save changes in a file, the system automatically updates the date and time. See Chapter 4 for details about editing and saving files.

+   - Refer to the sidebar Naming Directories (and Files) in this chapter for file-naming guidelines.