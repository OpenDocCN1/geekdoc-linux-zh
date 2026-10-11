Complete the following:

+   1. Verify that you are logged in to your system.

+   2. If necessary, switch to your root user account with the `su` command.

+   3. Change to the /RandD directory by entering `cd /RandD` at the shell prompt.

+   4. Create a design document for your team and restrict access to it by doing the following:

+   a. Create a new file named design_doc.odt by entering `touch design_doc.odt` at the shell prompt.

+   b. At the shell prompt, enter `ls -l`. Notice that the root user account and the root group are the owners of the new file.

+   c. Change ownership of the file to your user account and the research group using the `chown` command.

+   d. Enter `ls -l` again at the shell prompt. Verify that ownership of the file directory has changed to your user account and the research group. Notice that Owner has `rw-` permissions to the file, but Group only has `r--` permission.

+   e. Grant Group `rw-` permissions by entering `chmod g+w design_doc.odt` at the shell prompt.

+   f. Enter `ls -l` again at the shell prompt. Notice that Owner and Group now both have read/write access to the file.

+   g. Notice that Others have read access to the file. You need to keep this document confidential, so remove this access by entering `chmod 660 design_doc.odt` at the shell prompt.

+   h. Enter `ls -l` again. Verify that Others have no permissions to this file.

+   5. Next, you need to control access to the research directory itself using permissions. Do the following:

+   a. At the shell prompt, enter `cd ..`

+   b. At the shell prompt, enter `ls -l`. Notice that Owner has full access to the RandD directory, but Group is missing the write permission to the directory. Also notice that Others can read the directory contents (`r`) and can enter the directory (`x`).

+   c. Grant Group full access to the directory and remove Others access to the directory completely by entering `chmod 770 RandD` at the shell prompt.

+   d. Enter `ls -l` at the shell prompt. Verify that Owner and Group have full access while Others has no access.

Next, let's discuss how to work with default permissions.