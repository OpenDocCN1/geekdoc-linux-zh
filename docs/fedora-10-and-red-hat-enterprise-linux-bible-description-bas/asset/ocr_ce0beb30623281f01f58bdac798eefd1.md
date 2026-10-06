# Chapter 14: Computer Security Issues 577

# # Choosing good passwords

A good way to choose a strong password is to take the first letter from each word of an easily remembered sentence. The password can be made even better by adding numbers, punctuation, and varied case. The sentence you choose should have meaning only to you, and should not be publicly available (choosing a sentence on your personal Web page is a bad idea). Table 14-1 lists examples of strong passwords and the tricks used to remember them.

# Table 14-1: Ideas for Good Passwords

| Password | How to Remember It |
|---|---|
| Mrci7yo! | My rusty car is 7 years old! |
| 2Embpl | 2 elephants make BAD PETs, 1 is better |
| ItMcGib | Is that MY coat? Give it back |

The passwords look like gibberish, but are actually easy to remember. As you can see, I can place emphasis on words that stand for capital letters in the password. You set your password using the password command. Type the password command within a command shell, and it will enable you to change your password. First, it will prompt you to enter your password. To protect against "shoulder surfing" and learning your password, the password will not be displayed as you

As long as you use your old password correctly, the password command will prompt you for the new password. When you type in your password, the password command checks the password against cracklib to determine if it is a good or bad password. Non-root users will be required to try a different password if the one they have chosen is not a good password. The root user is the only user permitted to assign passwords. Once the password has been accepted by cracklib, the password command will ask you to enter the new password a second time to make sure there are no typos (which are hard to detect when you can't see what you are typing). When running as root, it is possible to change a user's password by supplying that user's login name as a parameter to the password command. Typing this:

```
$ password joe
```

results in the password command prompting for joe's new password. It does not prompt you for his old password in this case. This allows root to reset a user's password when user has forgotten it (an event that happens too often).

# # Using a shadow password file

In early versions of UNIX, all user account and password information was stored in a file that all users could read (although root could write to). This was not generally a problem because the password information was encrypted. The password was encrypted using a trapdoor algorithm, making the non-encoded password could be encoded into a scrambled string of characters, but the string could not be translated back to the non-encoded password.