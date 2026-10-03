# Apply Your Knowledge

4. A list of User Management tools appears in the right panel. Click the Administrative Roles tool.

5. Click Action in the toolbar located at the top of the SMC window. From the pull-down menu, click Add Administrative Role. The Add Administrative Role window appears. Fill in the fields with the following information:

Role Name: adminusr
Full Name: Administrative Assistant
Description: Admin assistant for performing general administrative tasks
Role ID number: <accept the default>
Role Shell: Administrator's Bourne

6. The next screen asks you to enter a role password. Enter a password that is 6–15 characters long. Click the Next button to proceed.

7. The next window is where you assign the rights. In the middle pane, select System Administrator and click the Add button. Under the Granted Rights pane, it should display System Administrator. Click the Next button to continue.

8. Select a home directory, and click the Next button.

9. In the next window, titled Assign Users to This Role, enter admin1 in the first field, and click the Add button. Click the Next button to continue.

10. When the summary window appears, click the Finish button. The process of assigning a role to a user is complete.

11. Log out and log back in as admin1. Start up SMC, and test the new user role. You should have general system administration privileges such as adding new users, scheduling jobs, and sharing file systems.

# Review Questions

1. Which three statements about Solaris Management Console are true?
A. It provides a graphical means to manage meta devices.
B. It simplifies administration by bringing the system administration tools together in one location.
C. It allows management of all Solaris Management Console servers in one location.
D. It allows a system administrator to delegate administrative tasks to non-root users without giving out the root password.

2. AdminSuite 3.0 is used to accomplish which of these tasks? Choose all that apply.
A. Manage user accounts
B. Manage shared resources
C. Manage disks
D. Manage processes
E. Schedule processes
F. Manage serial ports
G. Set up AutoClients