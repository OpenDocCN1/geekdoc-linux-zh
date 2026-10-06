# Administrator Accounts

The default administrator account has administrative privileges, and hackers frequently seek to obtain the logon information for an administrator account. Guessing a logon is a two-fold process of first identifying the username, and then the password. Default accounts allow the hacker to bypass the first half of this process.

Administrators should disable this account. If you double-click on any account (recall the Users groups previously shown in Figure 8-3) you will see a screen like that shown in Figure 8-5. From here you can disable the default administrator account.

![](bbox=[0.172, 0.307, 0.613, 0.676])

FIGURE 8-5 Disabling the default administrator account

Obviously, having an account with administrative privileges is necessary for maintaining your server. The next step is adding a new account, one with an innocuous name (for example, temp_clerk, receptionist, etc.), and giving that account administrative privileges. Doing so makes a hacker's task more difficult, as he must first ascertain what account actually has administrative privileges before he can even attempt to compromise that account.

Some experts suggest renaming the administrator account, or using an administrator account that has a username that indicates its purpose. That is not the recommendation of this book for the following reasons: