**Note** Historically, Unix systems have set their clocks according to UTC, or the time in Greenwich, England, and have adjusted local time settings based on the computer's location in the world. x86 PCs, by contrast, have historically set their clocks to the local time. Linux therefore needs to understand both methods. A dedicated Linux server is generally best off with its hardware clock set to UTC, because this is less likely to result in problems for various Linux utilities derived from Unix utilities or when Daylight Savings Time changes are required. However, the log entries will also use UTC timestamps, and this can be confusing. A system that dual-boots between Linux and Windows or some other OS that uses a hardware clock set to local time is better off using local time, to keep time synchronized between the OSes.

# ## Configuring User Accounts

You'll need to set up an account to access when the system is rebooted; you'll do that in the Account Configuration dialog box shown in Figure 2.5. You are required to set up the root account. This process consists of specifying and verifying root's password. You can then either click Next to continue or add one or more normal user accounts. It's a good idea to set up at least one user account, so that you are not forced to log in as root. To do so, input the account name (username), the password for that account, the same password again for verification, and the full name of the user. At this point, you may continue to add other users or continue to the next screen, Selecting Package Groups. You have several options for creating new users after the system has been installed. See Chapter 6 for more information about creating user accounts.

![](bbox=[0.11, 0.42, 0.76, 0.79])

**Figure 2.5:** The Account Configuration screen

# ## Selecting Package Groups

Finally, the moment you've waited for: the Selecting Package Groups screen allows you to select which software packages will be installed on your system, selecting them in preset server groups or individually. The only group that is selected by default for the server class installation is the Classic X Window System group. Many system administrators do not install any X Window System components on some of their servers, but the option is there. You can also choose to install a news

48