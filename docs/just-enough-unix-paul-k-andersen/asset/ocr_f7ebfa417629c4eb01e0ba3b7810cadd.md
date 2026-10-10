# 24.3    Removing Files Safely: del

The `rm` command can be very dangerous because it allows you to remove a file, but does not give you a way of getting back a file you may have removed accidentally. If you are a `csh` or `ksh` user, you can create an alias for the `rm` with the `-i` ("interactive") option; it will ask you if you are sure you want to remove the file in question. But `sh` does not allow aliases. Let’s create a script that will duplicate the effect of the `rm -i` command. The script will also tell what action has taken.

+   Listing 24-3A
+   Summary of the `del` script.

```
```
NAME
del - delete a file interactively
SYNOPSIS
del filename
DESCRIPTION
This is the outline for `del`:
Select `sh`
Get the filename from the command line (`$1`)
If there is no file with that `name`
print an error message.
Otherwise
Ask if the user wants to delete the file
Read the user’s choice (y/n)
If the choice is yes (y)
remove the file & print a message
otherwise
print a message
```
```

After studying the outline, create the script:

+   1.  **Use the text editor to create the script file.** Open a file named `del` and enter the script shown in Listing 24-3B. Write and quit the file when finished.

+   2.  **Make the script executable.** Use `chex` for this:
+   ```
+   $ chex del (Return)
+   del is now executable:
+   -rwx-r-x- 1 yourlogin 347  Date time  del
+   ```

+   3.  **Test the new script.** Use `del` on a file you no longer need.