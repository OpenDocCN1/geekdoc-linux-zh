At the adduser prompt, enter the login name that you want to create. It is advisable to use all lowercase letters to avoid confusion. Do not exceed the eight-character limit at this point. (Although a mixed case login can be useful for confusing people trying to hack into your system, it causes problems when your system tries to talk to others over a network.)

For our sample user account in this chapter, let’s create the user **fido**. (After all, as the joke goes, “On the Internet, no one knows if you’re a dog!”) Of course, you can substitute your choice on the screen in place of fido (unless you really like our login name).

```
Enter login name for new account (^C to quit): **fido**
Editing information for new user [fido]
Full Name:
```

After entering the login name, a status message from the adduser utility usually appears, followed by a set of questions about the new user and the type of environment to present the account with when the user logs in. (The exact order of questions may be different, but usually most of the same information is requested.)

In the example previously shown, the adduser routine is waiting for the user’s real name. At this prompt, type the full name of the user. Uppercase, lowercase, mixed case, and spaces are fine. This information is not mandatory but is used by the system for some other tasks. Other users can also identify you with this name when you are on a network.

```
Full Name: **Fido Dog**
GID [100]:
```

The system is waiting for you to provide a GID or *Group ID*, which is discussed in more detail in Chapter 35, “Users and Logins.” The last part of the prompt, [100], means that it’s suggesting a GID of 100. This is the default choice and is good for most systems unless you are part of a larger network which has a naming policy in effect. For most users, the default is a great way to start and you can always change it later if you need to.

# Tip

In this adduser utility and many other Linux programs, default choices are presented in square brackets. Simply press the Enter key to accept the default, or type the new value if you don’t want to accept the default value.

Sometimes (as you will see later in the adduser utility) you are given two choices—usually y for yes and n for no—separated by a / or | character. The uppercase letter is the default choice which you can select by pressing Enter. The other choice must be typed explicitly. In the following examples, yes is always the default choice: [Y/n], [Y;n], [Yn].