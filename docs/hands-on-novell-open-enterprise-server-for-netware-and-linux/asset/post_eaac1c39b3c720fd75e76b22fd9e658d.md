
- b. Enter the login script commands shown in Figure 9-19.
- c. Click OK to save the login script and return to the main ConsoleOne window.

5. Exit ConsoleOne, and log out.

6. In the Novell Login window, change the context to the IT OU and enter Eric Kenton’s user name and password.

7. Follow these steps to set login script options in Novell Client:
   - a. Click the Advanced button, and then click the Script tab to display the options shown previously in Figure 9-17.
   - b. If necessary, click to clear the Close automatically check box and click to select the Display results window check box.

8. Click OK to log in. A results window should be displayed with the welcome message you entered in your login script.

9. Press the spacebar to continue. The drive mappings are then added to the results window. Record the drive mappings and list any drive letters that are repeated:

> NOTE
> Repeated drive letters could mean that the default login script is running or that the user has a user login script that’s changing drive mappings. You learn how to disable the default login script in Activity 9-9.

10. Close the results window, and log out.

11. Change the Novell Client login options and repeat the login process:
    - a. In the Novell Login window, click the Advanced button, and then click the Script tab.
    - b. Click to select the Close automatically check box.
    - c. Click OK to log in.

12. Record the contents of the results window:

13. Close any open windows, and log out. Leave your system running for the next activity.

## Login Script Variables

As with other programming languages, the NetWare login script language allows using variables in many commands. A **login script variable** is a reserved word in the login script language, and its value can change for each user login. With login script variables, you can write one login script that works for many different users and computers. Login script variables can be divided into types based on their use: date variables, time variables, user variables, and workstation variables, explained in the following sections.

> NOTE
> Remember to use all uppercase letters for a variable and precede it with a percent sign (%), as explained in “Using Login Script Variables” later in this chapter. For more information on login script commands and variables, check Novell’s Web site (http://novell.com).

### Date Variables

**Date variables** contain information about the current day of the week, the month, and the year in a variety of formats, as shown in Table 9-4. Date variables can be useful for displaying current date information or to check for a specific day to perform tasks. For example, the Engineering Department needs to meet at 10:00 a.m. each Monday to review weekly work projects. Using the DAY_OF_WEEK variable, you could display a message on Monday morning reminding them of the meeting. The values for date variables are stored as fixed-length ASCII strings.

**Table 9-4 Date variables**

| Variable | Description |
| :--- | :--- |
| DAY | Day of the current month in number format, with possible values from "01" to "31" |
| DAY_OF_WEEK | Name of the current day of the week, with possible values of "Monday," "Tuesday," and so on |
| MONTH | The current month in number format, with possible values from "01" for January to "12" for December |
| MONTH_NAME | The name of the current month, with possible values from "January" to "December" |
| NDAY_OF_WEEK | The current weekday in number format, ranging from "1" for Sunday to "7" for Saturday |
| SHORT_YEAR | The last two digits of the current year, such as "05" or "06" |
| YEAR | The full four-digit year, such as "2005" or "2006" |

### Time Variables

The time variables, shown in Table 9-5, offer a variety of ways to view or check the login time.

**Table 9-5 Time variables**

| Variable | Description |
| :--- | :--- |
| AM_PM | Used to specify day or night (possible values of "am" or "pm") |
| GREETING_TIME | Used for displaying welcome messages, with possible values of "Morning," "Afternoon," or "Evening" |
| HOUR | The current hour of the day or night in the range of "01" through "12" |
| HOUR24 | The current hour in 24-hour mode, ranging from "01" to "24" |
| MINUTE | The current minute, ranging from "00" to "59" |
| SECOND | The current second, ranging from "00" to "59" |

The GREETING_TIME variable is most often used in WRITE statements to display welcome messages. The HOUR variable requires using the AM_PM variable to determine whether the time is before or after noon, so the HOUR24 variable is often easier to use.

### User Variables

The user variables, shown in Table 9-6, allow you to view the user's login name, full name, or hexadecimal user ID specified in eDirectory.

**Table 9-6 User variables**

| Variable | Description |
| :--- | :--- |
| FULL_NAME | The user's full name, as defined in the user properties |
| LOGIN_NAME | The user's unique login name |
| USER_ID | The hexadecimal number NetWare assigns to the user login name |
| HOME_DIRECTORY | The path to the user's home directory |

LOGIN_NAME and FULL_NAME can be used to personalize greeting messages. You use the HOME_DIRECTORY variable in Activity 9-9 to automate mapping drive H: to a user's home directory.

## Workstation Variables

**Workstation variables**, shown in Table 9-7, are most often used to establish drive mappings for software directories according to the client computer's hardware or OS.

**Table 9-7 Workstation variables**

| Variable | Description |
| :--- | :--- |
| OS | The computer's operating system; the default value is “MSDOS” |
| OS_VERSION | The version of DOS used on the computer processing the login script |
| MACHINE | The long machine name that can be assigned in the Shell.cfg or Net.cfg file; the default value is “IBM_PC” |
| P_STATION | The node address of the computer's network card, expressed as a 12-digit hexadecimal value |
| SMACHINE | The short machine name that can be assigned in the Shell.cfg or Net.cfg file; the default value is “IBM” |
| STATION | The connection number assigned to the user's computer; sometimes used by software packages to separate the user's temporary files when multiple users are working in the same shared directory |
| SHELL_TYPE | The computer's shell version number |
| NETWORK_ADDRESS | The IPX address of the cable the user's computer is attached to, expressed as an 8-digit hexadecimal number |
| FILE_SERVER | The name of the current file server |

## Using Login Script Variables

To see how login script variables work, in this section you use them to display the current date in the greeting message and assign a drive pointer to each user's home directory in the IT OU. Without login script variables, you would have to create a separate script for each user containing a MAP command to his or her home directory, as shown in Figure 9-20. As you can see, creating a separate login script for each user involves a lot of extra work and redundancy.

An alternative is creating a single container login script that works for all users in the OU. As you learned in Chapter 5, each user's home directory is given the same name as the user's login name by default, which you can see in Figure 9-20. The path to the user's home directory is then stored as a property of the user account in eDirectory. When users' home directory paths are included with their user account information, you can reduce the number of statements in the login script by using the HOME_DIRECTORY variable in the MAP command:

```
MAP ROOT H:=%HOME_DIRECTORY
```

The percent sign in front of the variable name is necessary to tell Novell Client to substitute the path to the user's home directory for the HOME_DIRECTORY variable during login. Notice, too, that the variable name is in all uppercase letters.

> Because many login script commands require capitalizing variable names, it's a good practice to capitalize *all* login script variable names.
