# Task: Creating a Strategy for Choosing Passwords

If they are properly selected and frequently changed, passwords can be a major deterrent to someone trying to obtain unauthorized access to your account. Here are the guidelines that you should follow when choosing passwords for the superuser and unprivileged user account:

+   1. Use a mix of uppercase and lowercase letters, numbers, and symbols.
+   2. Do not use dictionary words and, in particular, do not use English words. If you can find the word in a dictionary, don't use it as a password.

![](bbox=[0.1, 0.5, 0.18, 0.58])

> Passwords should not be someone's name, either. Don't use the names of favorite pets, old lovers (or new ones), friends, enemies, birthdays, or phone numbers. It has been mentioned that it is really a simple matter to determine your great-grandmother's maiden name on either your father or mother's side of the family.

+   3. Passwords must be easy to remember and quick to type. They must also be hard to figure out.
+   4. Passwords should be at least eight characters in length.
+   5. Passwords can be made to appear to be words, if that makes them easier to remember—the password 2hfArEe (tooth fairy) is a good example, but it isn't a very good password anymore, now that it's been put in this book.
+   6. Test your passwords before you use them. Type the following on the command line:
+      echo password | ispell -l
+      Replace the word password with the password you chose. Figure 3.1 shows a few attempts at selecting good passwords.
+   7. Educate those people who will be using the system on how to select a sound and secure password.

```
echo password | ispell -l
```