# Passwords—A Key Point for Good Security

Sheesh, this seems to leave KH*^&)g# and equally impossible-to-remember passwords. Pick two or three unrelated words, add in at least two nonalphanumeric characters such as punctuation or control characters, and capitalize one or more letters in the words other than the first letter of each word.

There is an additional variation used for account passwords in Linux and UNIX, called the salt. This means that whenever a password is created for an account, two random characters, called the salt, are generated and are added to the password before encryption to add an additional permutation. When the password is stored in /etc/passwd or /etc/shadow, these two salts are prepared to the encrypted password.

The reason for the salt is that even if the same password is used by two users on a system or by the same user on different systems, the encrypted password is for each different. The purpose is to prevent the mass cracking of passwords. Before the salt technique was added, a cracker would generate the encrypted password for, say, each word in a dictionary and compare the encrypted password to that of each user's password in /etc/passwd. Thus, if there were 100 accounts, only the cracker had to encrypt that password from the dictionary.

However, because each of those 100 users has different salt, no longer works. For each cracker, the master must extract the salt from /etc/passwd or /etc/shadow, add that to the dictionary, encrypt, and compare to that user's encrypted password. Thus, the cracker's effort is multiplied by the number of accounts, 100 in this example.

Some of the following good passwords. In each case intermix with lower characters and capitalize other than the first letter, for example:

```
vote\z0r0
```

+   - The first or second letter from each word of an obscure phrase
- An unusual word from one category such science fiction and an unusual and unrelated word from another category such politics. No, phaser->Gore or phaser->Bush is not a good password.
- The name of your first crash and first computer (if different)
- A musical group or song if uncommon and your mother's birthdate (your brother's birthdate would not be good because he may know your musical preferences; moms usually do not)
- An old phone number or street address and a roommate from long ago's last name or peculiarity
- Ideas from looking around your bookshelf and office for disparate names to combine

The password also should be one that can be memorized so it does not need to be written down. Passwords should not be written down, especially not on paper near the terminal or where someone might know to look for it. They should be stored on a computer or magnetic or optical media unless in a suitably encrypted form.

A password that is used for a high-security application should also not be used as the password for a low-security application nor should it be used in unrelated high-security applications. A high-security application would be where money or very confidential information