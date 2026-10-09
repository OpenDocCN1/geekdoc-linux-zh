# ACTIVITY 5-1

# Modifying File and Directory Permissions Using the Command Line

Data Files:
Training_Policy.txt

Before You Begin:

+   1. You have logged in as root in the CLI.
2. Enter `cd /root` to change to the root directory.
3. Enter `cp -p /085039Data/Linux_Permissions/* /root` to copy the files.
4. Enter `chmod 700 Training_Policy.txt` to change the file permissions.
5. Enter `clear` to clear the terminal screen.

Scenario:

A new employee training policy is to be implemented in your organization and your human resources manager wants all employees to be able to read the newly created Training_policy.txt policy document. You have been assigned the task of allotting permissions to all users so that they can read the file.

What You Do

How You Do It

+   1. View the permissions of the Training_Policy.txt document.

+   a. Enter `ls -l` to view the permissions of the Training_Policy.txt file.
b. Observe that the root user has read, write, and execute permissions on the Training_Policy.txt file, while the group and others do not have any permissions.