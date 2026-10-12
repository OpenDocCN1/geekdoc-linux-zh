programs to reveal your secrets\-the weak passwords. So, cracking your own passwords before hackers do can help you to eliminate weak passwords.

# ## How passwords are cracked

The best way to understand the cryptic details of cryptography is to use an example. If you create a new user on your system with a username bob and password umbrella, you will see a line in the /etc/passwd file that looks something like the following line:

```
bob: XoAlxlaie wp8s: Red Hat Linux User: /home/ bob: /bin/ bash
```

The line may not look quite the same, but the point is that you will have a line with bob's encrypted password. The encrypted password is a 13-character string created by a function called crypt() as follows:

```
Encrypted Password = crypt('xoAlxlaie wp8s', "umbrella", salt)
```

The salt is a two-character string chosen from a set of $[a\text{-}zA\text{-}Z0\text{-}9\text{\_} /$ . This string is used to influence the encryption algorithm in one of 4,096 different ways. The salt value is stored in the encrypted password as the first two characters. For example, the X o in **xoAlxlaie wp8s** is the encrypted password for umbrella, the salt value used is X o. No known way exists of retrieving the original password from the encrypted version, because the encryption algorithm is one-way only.<sup>2</sup>However, if the encrypted password is known, then a program can be written to use the two-character salt value and encrypt a large dictionary of words with this salt. If the password happens to be a word in the dictionary, as it is in this example, it will be salted and a match will be found. In other words, when you know that the salt value for bob's password is X o, you can use this salt to write a program to do the following:

```
Encrypted Password = crypt(each dictionary word, Xo)
```

When this program chooses the word "umbrella," the encrypted password will be same as the one stored in /etc/passwd. Too bad, bob's password has just been cracked! Now the program knows which word (umbrella) was used to create the password. This is the simplified explanation of how cracking software works. However, bear in mind that today's cracking software is much more advanced, and as computer hardware becomes more and more powerful, cracking passwords becomes easier and faster.