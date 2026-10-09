> In general, don't use the root account unless you need to use it.

If you're worried about the hassle of logging in and out of different accounts, then worry no more. Linux allows you to run a root shell from within your normal account, so that you can do most of your work under the normal account and switch to the root shell for those sensitive administration-level activities. We'll talk about that later in this chapter.

# # The Red Hat User Manager

In this section, we'll have a look at some of the most common tasks in user account management: creating user accounts and groups, and adding a user account to a group. We'll use the graphical **Red Hat User Manager** tool to step through some examples. Then, in the next section, we'll look at what's happening under the covers – we'll check the impact of our actions on the relevant configuration files and learn how to perform the same (and other) operations via the command line.

To try the **Red Hat User Manager**, we'll need to use the root account (and to be extra careful!) at each step. We'll assume that you're logged in with a non-root account, which (as we've already mentioned) is the safest way to use your operating system.

When you launch any of Red Hat Linux's graphical administration tools from a non-root account, Linux will (if necessary) prompt you to enter the password to the root account. The figure below shows the window you'll see every time the root password is required by a graphical tool:

![](bbox=[0.24, 0.59, 0.78, 0.77])

If the password is accepted, a key-shaped icon will appear in the notification area at the bottom right corner of the screen. As long as that icon remains displayed, you can start other Red Hat Linux graphical administration tools without being asked again for the root password. The key icon does not mean that all actions are undertaken with root privileges; it simply means that when an administration tool requires the root account to run, it may skip this step because the user has already provided the password.