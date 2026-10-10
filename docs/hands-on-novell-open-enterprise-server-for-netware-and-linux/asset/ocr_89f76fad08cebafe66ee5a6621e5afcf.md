+   b. Enter the login script commands shown in Figure 9-19.

+   c. Click OK to save the login script and return to the main ConsoleOne window.

+   5. Exit ConsoleOne, and log out.

+   6. In the Novell Login window, change the context to the IT OU and enter Eric Kenton’s user name and password.

+   7. Follow these steps to set login script options in Novell Client:

+   a. Click the Advanced button, and then click the Script tab to display the options shown previously in Figure 9-17.

+   b. If necessary, click to clear the Close automatically check box and click to select the Display results window check box.

+   8. Click OK to log in. A results window should be displayed with the welcome message you entered in your login script.

+   9. Press the spacebar to continue. The drive mappings are then added to the results window. Record the drive mappings and list any drive letters that are repeated:

> NOTE
> Repeted drive letters could mean that the default login script is running or that the user has a user login script that’s changing drive mappings. You learn how to disable the default login script in Activity 9-9.

+   10. Close the results window, and log out.

+   11. Change the Novell Client login options and repeat the login process:

+   a. In the Novell Login window, click the Advanced button, and then click the Script tab.

+   b. Click to select the Close automatically check box.

+   c. Click OK to log in.

+   12. Record the contents of the results window:

+   13. Close any open windows, and log out. Leave your system running for the next activity.

# ### Login Script Variables

As with other programming languages, the NetWare login script language allows using variables in many commands. A **login script variable** is a reserved word in the login script language, and its value can change for each user login. With login script variables, you can write one login script that works for many different users and computers. Login script variables can be divided into types based on their use: date variables, time variables, user variables, and workstation variables, explained in the following sections.

> NOTE
> Remember to use all uppercase letters for a variable and precede it with a percent sign (%), as explained in “Using Login Script Variables” later in this chapter. For more information on login script commands and variables, check Novell’s Web site (http://novell.com).

# ### Date Variables

**Date variables** contain information about the current day of the week, the month, and the year in a variety of formats, as shown in Table 9-4. Date variables can be useful for displaying current date information or to check for a specific day to perform tasks. For example, the Engineering Department needs to meet at 10:00