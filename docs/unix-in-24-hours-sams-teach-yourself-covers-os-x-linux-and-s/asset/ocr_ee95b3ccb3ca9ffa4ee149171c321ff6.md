where `taylor` is the account name and `intuitive.com` is the name of the remote host. If that’s how you need to access your Unix system remotely, it’s actually easier than using the login/password sequence; you just need to make extra sure that you type in everything exactly as prompted.

+   3. At the login prompt, enter your account name if needed:

```
login: **taylor**
Password:
```

*Be particularly careful to use exactly what your administrator tells you to use* (for example, the accounts `taylor`, `Taylor`, and `TAYLOR` are all different to Unix). After you’ve entered your account name, the system moves the cursor to the next line and prompts you for your password. If you’re using the `ssh` sequence, then the prompt will include your account name, as shown here:

[Click here to view code image](#)

```
taylor@intuitive.com’s password:
```

Either way, when you enter your password, the system won’t echo it (that is, won’t display it) on the screen. That’s okay. Lack of an echo doesn’t mean anything is broken; instead, this is a security measure to ensure that even if people are looking over your shoulder, they can’t learn your secret password by watching your screen. Be certain to type your password correctly because you won’t see what you’ve typed and have a chance to correct it.

# Note

If you enter either your login or your password incorrectly, the system complains with an error message:

```
login: **taylor**
Password:
Login incorrect
login:
```

Most systems give you three or four attempts to get both your login and password correct, so try again. Don’t forget to enter your account name at the login prompt each time, as required. Be careful, though: Too many failed login attempts, and you might lock out your account and have to contact the administrator for help.

+   4. After you’ve successfully entered your account name and password, you are shown some information about the system, some news for users, perhaps a fortune, and an indication of whether you have electronic mail. The specifics will vary, but here’s an example of what I see when I log in to my account:

[Click here to view code image](#)

```
login: **taylor**
Password:
Last login: Thu Jul 7 17:00:23 on ttyAe
You have mail.
$
```