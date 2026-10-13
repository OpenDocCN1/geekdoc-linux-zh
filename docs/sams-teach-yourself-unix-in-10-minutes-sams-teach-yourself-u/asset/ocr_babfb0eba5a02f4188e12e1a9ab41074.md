# LESSON 15
User Utilities

![](bbox=[0.55, 0.1, 0.9, 0.28])

*In this lesson you will learn how to change your password and shell, and to modify other information.*

UNIX provides a wealth of utilities to help you control the information that the system stores for your user account. In this lesson, you'll see how to monitor the use of your system through some useful command-line utilities.

# CHANGING YOUR PASSWORD: passwd AND yppasswd

One of the most important things you'll need to do in a networked environment is change your password. Passwords generally need to be changed somewhat frequently in order to maintain a secure environment.

There are two ways that a password can be changed. If you are in a networked environment you might have to use the yppasswd, which updates your password on all the networked machines. The most obvious way of telling if this is the sort of environment you're working in is if you can log into multiple computers with the same username and password and access the same information. This is a common setup for UNIX computer labs. If your machine is an isolated UNIX computer, just use the passwd command and you will be fine. The two commands operate in an identical manner, it is simply where the updated password is stored that is different.

For example, type the following:

```
>passwd
Changing password for jray
Old password: *****
New password: *****
Retype new password: *****
Password successfully changed
```