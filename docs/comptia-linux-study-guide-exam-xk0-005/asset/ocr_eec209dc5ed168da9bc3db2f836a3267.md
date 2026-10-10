![](bbox=[0.128, 0.109, 0.339, 0.268])

An old troubleshooting technique is to break a problem in half: if the cause is not in the first half, it's in the second half. Break the second part in half and continue to analyze. In this chapter, we're splitting user issues into system access and file difficulties. We further divide these problem categories while stepping you through various items to consider as you move toward a solution.

# # Troubleshooting Access

If a user is having trouble accessing their desired applications, a mixed bag of authentication issues can be the cause. We'll take a look at local and remote access as well as authentication scenarios.

# ## Local

Local access refers to those users who are using a directly connected interface to the server. These are typically server administrators but may be application users as well. Begin troubleshooting by gathering some basic information:

+   - Is this a newly created user account?
+   - What is the username being entered for the account?
+   - Has the user ever logged into the account?
+   - Is the user attempting to log in via the GUI or a text-based (virtual) terminal (for example, tty2)?

# ### Checking a Newly Created User Account

If the account is a newly created account, confirm that it was properly built. New system administrators often create user accounts with the `useradd` command (see Chapter 10, “Administering Users and Groups”) but forget to add its password with the `passwd` utility. Use either the `grep` or the `getent` command to check the `/etc/passwd` and `/etc/shadow` file records. An example is shown in Listing 22.1 for a new user account, `JKitRk`, on an Ubuntu Desktop distribution.