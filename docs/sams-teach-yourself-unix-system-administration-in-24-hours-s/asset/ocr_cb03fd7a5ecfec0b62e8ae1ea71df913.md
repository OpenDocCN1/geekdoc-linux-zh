while Linux uses the command chage. There's no equivalent mechanism in Mac OS X/Darwin, nor does Darwin support the shadow password file mechanism.

1. Let's start with chage, because it makes the various possible settings quite obvious:

```
# man chage | head -12
CHAGE(1)                                                                 CHAGE(1)

NAME
    chage - change user password expiry information

SYNOPSIS
    chage [-m mindays] [-M maxdays] [-d lastday] [-I inactive]
    chage [-E expiredate] [-W warndays] user
```

The -l flag is a good place to start, as it generates a report of password aging information for the specified account and can be used by anyone:

```
$ chage -l taylor
Minimum:           0
Maximum:           99999
Warning:            7
Inactive:          -1
Last Change:       Jan 14, 2002
Password Expires:  Never
Password Inactive: Never
Account Expires:   Never
```

As you can see, taylor is in luck; the password never expires, and the account never expires, either. The first four fields deserve an explanation, however.

The Minimum and Maximum fields are the minimum and maximum number of days between password changes—quite literally. If the minimum was two days and user taylor changed his password early one morning, he couldn't change it again until the minimum number of days value had elapsed.

The Warning field indicates the number of days before the password expires that the user will be warned during the login process, and, finally, the Inactive field indicates how many days after a password expires that the account will automatically be locked (similar to passwd -l).

2. Remember our friend testtude? It's time to make some changes to his account to match the account password policy implemented at our site.

The first update is that passwords must be changed every 30 days, and that if the user doesn't log in within 14 days of the expiration date of their password, the account should be automatically locked out. The testtude account should have a two-day warning before being forced to change the password upon login, and it's also due to expire on August 3, 2003, so that'll be specified too.

![](bbox=[0.88, 0.72, 0.99, 0.88])