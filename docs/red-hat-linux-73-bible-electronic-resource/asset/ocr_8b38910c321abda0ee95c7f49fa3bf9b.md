+   * Do not use a dictionary word, even if you add numbers or punctuation to it.
+   * Do not use proper names of any kind.
+   * Do not use any contiguous line of letters or numbers on the keyboard (such as “qwerty” or “asdfg”).

# # Choosing good passwords

A good way to choose a strong password is to take the first letter from each word of an easily remembered sentence. The password can be made even better by adding numbers, punctuation, and varied case. The sentence you choose should have meaning only to you, and should not be publicly available (choosing a sentence on your personal Web page is a bad idea). Table 14-1 lists examples of strong passwords and the tricks used to remember them.

**Table 14-1: Ideas for Good Passwords**

| Password | How to Remember it |
|:---|:---|
| Mrcl7yo! | My rusty car is 7 years old! |
| 2emBp1ib | 2 elephants make BAD pets, 1 is better |
| ItMc?Gib | Is that MY coat? Give it back |
| | |

As you can see, I even placed emphasis on particular words and used that to remember capitalization of certain letters. The passwords look like gibberish, but are actually rather easy to remember. You set your password using the passwd command. Type the passwd command within a command shell, and it will enable you to change your password. First, it will prompt you to enter your old password. To protect against someone “shoulder surfing” and learning your password, the password will not be displayed as you type.

Assuming you type your old password correctly, the passwd command will prompt you for the new password. It will ask you to enter the new password a second time to make sure there are no typos (which are hard to detect when you can’t see what you are typing). When running as root, it is possible to change a user’s password by supplying that user’s login name as a parameter to the passwd command. Typing this:

```
# passwd joe
```

results in the passwd command prompting you for joe’s new password. It does not prompt you for his old password in this case. This allows root to reset a user’s password when that user has forgotten it (an event that happens all too often).