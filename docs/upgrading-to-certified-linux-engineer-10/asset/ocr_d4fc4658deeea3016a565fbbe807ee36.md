# PAM Configuration

Each line in a PAM configuration file contains 3 columns plus optional arguments:

Figure 6-2

![](bbox=[0.33, 0.3, 0.85, 0.7])

The following describes the purpose of each column:

+   - **Module Type.** There are four types of PAM modules:
+     - **auth.** These modules provide two ways of authenticating the user.
+       First, they establish that the user is who he claims to be by instructing the application to prompt the user for a password or other means of identification.
+       Second, the module can grant group membership or other privileges through its credential granting properties.
+     - **account.** These modules perform nonauthentication based account management.