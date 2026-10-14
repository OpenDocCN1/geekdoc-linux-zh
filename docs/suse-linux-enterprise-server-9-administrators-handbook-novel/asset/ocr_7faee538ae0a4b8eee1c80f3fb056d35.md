to company information can be removed at the same time the termination notice is given. When identity provisioning is used, all the users accounts should be automatically disabled upon HR setting the employment termination flag in that person's record.

Lastly, we would like to add a few words about system accounts that are not used by humans, but by applications. As previously discussed in Chapter 4, “User and Group Administration,” and Chapter 8, “Network Services,” whenever possible, system services should be run under unprivileged accounts instead of root. Some package installations create a user account to be used by the package. In all cases, you should ensure these application accounts are not given a usable shell, to prevent them from being used by intruders to access your system. We recommend that you set the shell for these accounts to `/bin/false`.

# TIP

You may want to add `/bin/false` to the list of available shells in `/etc/shell`. This way, when YaST is used to create a user, your account creation procedure for application accounts can specify that the `/bin/false` shell be selected from the drop-down list.

Regardless of how user accounts are created, either manually or via provisioning, ensure a clearly stipulated set of requirements exists on the minimum amount of user information that must be recorded in the user account record. For example, include location of home directory, groups the user belongs to, GECOS data (if any telephone numbers are to be included or not), and so on.

# Strong Passwords

Strong, secure passwords are a cornerstone of an effective security strategy. Passwords ensure that only authorized personnel will be able to gain access to system resources. Unfortunately, this is not always the case. The individuals who are utilizing these resources choose most passwords and, as a result, the words, symbols, or dates that make up the passwords usually have some personal meaning to the users so they are easier to remember. Herein lies the problem. Because of human nature, convenience is often chosen over security. As a result, users choose passwords that are relatively simple. Although this helps them to remember the passwords, it also makes the passwords much easier for hackers to crack. The first line of security defense thus becomes one of the weakest.