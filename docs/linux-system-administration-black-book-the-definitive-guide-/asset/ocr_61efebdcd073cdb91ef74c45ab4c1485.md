Choose what information you want to include in your prompt. To use the username and the full path in your prompt, for example, include \u and \w.

+   8.  Choose the format you want this information to be in. Any characters that do not have a backslash associated with them are included literally. For example, if you want your prompt to end with a dollar sign and a space, then just tack these items on the end. You would also want to separate the two entries with a space.

+   9.  Complete the prompt statement. In the case of this example, you would have the following:

```
PS1="\u \w$ "
```

+   10. Press the Esc key to return to Command mode, and then type \"ZZ\" to save and close the file.

+   11. Log out from this shell instance and log back in. The new prompt should now be active.

> TIP: Set this file with executable permissions if you want to run it by typing \'/script\'.

# Writing Your Own Package Update Script

To learn how to write your own package update script, do the following:

+   1. Log in as root, because this script is meant to update all packages.

+   2. Type \"vi ~/bin/update.scr\" to open the script file for editing.

+   3. Type \"i\" to enter Insert mode.

+   4. Type the following to ensure that Linux knows that this is a bash shell script:

```
#!/bin/bash
```

+   5. Determine the FTP or Web site you want your script to get its information and files from. A default might be ftp.redhat.com. You might have the following line included to establish this connection:

```
ftp ftp.redhat.com
```

+   6. The script cannot send any instructions to the server until it is properly connected, so you need to choose a loop that makes it wait for this to happen. An until loop would serve this function well, so start with:

```
until [
```