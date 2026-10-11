the useradd utility. The following example shows how I create a user ID for my friend Bob:

```
useradd bob
```

I use Bob's first name as the user ID and I enter it in lowercase letters. I can use any letters or numbers for the user ID and also can use a mixture of upper- and lowercase or all uppercase letters. Bob's user ID, therefore, can also appear as any of the following variations (whichever one I may choose to make it):

```
Bob
BOB
bOb
BOB
```

![](bbox=[0.05, 0.35, 0.15, 0.45])

I prefer to keep user IDs simple, however, because Linux user IDs are case sensitive, which means that Linux treats each of the preceding four examples as unique user IDs—in addition to the original version, bob. All the user IDs that I create, therefore, are in lowercase, which enables users and me to remember them more easily.

After I press the Enter key, Linux prompts me to enter a password for the new user ID. Again, I like to keep things simple, especially because I'm creating this user ID to practice my e-mail programming. So I use the user ID as the password, too, as follows:

```
passwd bob
```

Don't get confused if you see passwd. Instead of using password as the prompt, Linux just uses passwd. (You notice that Linux likes to abbreviate.) Simply enter the password after the prompt and press the Enter key.

Don't get surprised if Linux becomes a little temperamental and yells at you, saying that it doesn't like the password you select. Linux doesn't like most of the passwords that you come up with because those passwords appear in the Linux dictionary. You can almost always expect to see the following message after you enter the password.

```
New Unix password: bob
BAD PASSWORD: it is based on dictionary word.
Retype new Unix password:
```

Of course, Linux substitutes your own password for the word bob in this example. This message is merely a warning, which you can ignore. Linux is simply telling you that a hacker can create a program that uses each word in the dictionary as the password. If your password is in the dictionary, the likelihood that a hacker can figure out your password is high.