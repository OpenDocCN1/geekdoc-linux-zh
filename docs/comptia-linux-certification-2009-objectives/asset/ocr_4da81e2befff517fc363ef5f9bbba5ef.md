4. Check whether the members of the Tax group are able to remove the Salaryaccount.txt file.

+   a. Log in as the income user.

+   b. Enter `cd /home/tax/Finance` to switch to the Finance directory.

+   c. Enter `ls` to view the contents of the directory.

+   d. Enter `rm Salaryaccount.txt` to verify if the Salaryaccount.txt file can be deleted.

+   e. Observe that a prompt with a message to confirm the removal of a rights protected regular file is displayed.

+   f. Enter `y` to confirm the removal of the file.

+   g. Observe that a message is displayed to indicate that permission is denied because the immutable flag for the directory is set.

+   h. Log out of the terminal.