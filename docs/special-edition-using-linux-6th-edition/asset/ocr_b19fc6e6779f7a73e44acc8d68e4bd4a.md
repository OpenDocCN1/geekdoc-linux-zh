```
col:pbHeh8NUW842:10573:0:-1:7:7:-1:1073897392
natalie:jEFpY1Zqmi8E.:10576:0:-1:9:-1:-1:1073897392
ryan:BhCkjWnhFk/:10576:0:-1:7:-1:1:1073897392
brittany:oCtbTK7DjDye2:10576:0:-1:9:-1:-1:1073897392
kelsey:dDULxtAbiJvAm:10576:0:-1:7:-1:1:1073897392
```

Much like the `/etc/passwd` file, the `/etc/shadow` file consists of single-line entries with colon-delimited fields. Some of these fields will contain seemingly bizarre numbers, too large to be correct. These fields have as their reference the “computing age epoch” date of Jan 1, 1970.

| Field | Description |
|---|---|
| 1 | User account name |
| 2 | Encrypted password field |
| 3 | Days elapsed since beginning of the epoch that password was last changed |
| 4 | Number of days that must elapse before password can be changed again |
| 5 | Number of days after which password must be changed (-1 means never) |
| 6 | Days before password expiration that user will receive warning when logging in |
| 7 | Days after password expires that the account is disabled if the password is not successfully changed |
| 8 | Days elapsed since epoch on which account will be disabled (regardless of password changes) |
| 9 | A reserved field |

You’ll use `change`, the change-aging utility, to change these values from the defaults, which are found in `/etc/login.defs` (see the following text).

# MD5 HASHED PASSWORDS

Most distributions are also offering the use of an MD5 hash rather than the older DES hash. This text will not delve into the details of the MD5 hash other than to mention that it allows longer passwords than the DES encryption. Longer passwords will only mean that the theoretical time to break the password is lengthened, but this only applies to good passwords. Bad passwords (those based on dictionary words or other common data) will be broken just as fast as they are with DES.

> **Caution:** If you are using NIS, you cannot use MD5. As of this writing, NIS cannot understand MD5 hashed passwords. This also applies to mixing systems using restricted services that use different password schemes. Ensure all your network programs work with MD5-hashed passwords before moving to them.