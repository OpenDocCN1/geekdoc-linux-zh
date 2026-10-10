guessed or otherwise discovered by a cracker, granting full access to your account (or the computer, in the case of the root password). Crackers can use network sniffers (tools to monitor network activity), social engineering (tricking people into revealing their passwords), dictionary attacks (encrypting every word in a dictionary and comparing the results to what’s stored in a stolen encrypted password file), and other techniques to break into a computer. Even a good password can be a risk if you write it down or store it on a disk file.

# Procedure

Generating a good password requires two main steps: First, you should select a base for the password. The base should be relatively easy to remember but hard to guess. Second, you should modify the base in various ways to make it even harder to guess. Once you’ve selected and implemented your password, you should take various steps to keep it from being compromised.

# Selecting a Solid Base

The password base is a string that’s memorable but that shouldn’t appear in any language’s dictionary as a single word. One reasonable procedure for picking a base is to use an acronym. For instance, you might use yiuutd, for yesterday I went to the dentist. (Of course, this specific example is a poor one because it’s been used as an example in this book. A cracker who reads this book might add yiuutd to a dictionary, and it might spread from there.) Another option for a base is to use two short and unrelated words, such as bunpen. You won’t find bunpen in a dictionary, although you will find its constituent words. (Again, this specific example is now a poor base because it’s appeared in this book.) A variant on the multiword approach is to use fragments of multiple words, such as asepho, derived from baseball and telephone. As a general rule, an acronym is the safest choice, providing it doesn’t happen to spell anything.

![](bbox=[0.15, 0.61, 0.23, 0.67])

> These examples are all six characters long. Subsequent modifications add characters, and passwords on some OSs are limited to eight characters in length, hence the six-character length. Modern Linux distributions are not so limited, and in fact eight characters is a more reasonable minimum safe password length than a maximum. You might need to generate short passwords for some purposes, though, such as for retrieving email from your ISP or logging onto Web pages.

There are many common types of strings you should never use as a password, or even as a password’s base:

+   *   The name of any relative, friend, co-worker, or pet
+   *   The name of any character in a book, movie, or play or the name of a favorite work of fiction or art
+   *   Your own name or your username
+   *   Any other personally relevant information, such as your Social Security number or street address