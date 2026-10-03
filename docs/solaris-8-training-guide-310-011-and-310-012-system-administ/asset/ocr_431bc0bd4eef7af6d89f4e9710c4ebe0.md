| Field Name | Description |
|---|---|
| comment | Usually contains the user's full name. |
| home-directory | Contains the user's home directory pathname. |
| login-shell | Contains the user's default login shell. |

Each line in the /etc/shadow file contains several fields separated by colons (:). This line is formatted as follows:

```
username:password:lastchg:min:max:warn:inactive:expire
```

Table 8.4 defines each field in the /etc/shadow file.

# TABLE 8.4

# FIELDS IN THE /ETC/SHADOW FILE

| Field Name | Description |
|---|---|
| username | Contains the user or login name. |
| password | Might contain the following entries: a 13-character encrypted user password; the string *LK*, which indicates an inaccessible account; or the string NP, which indicates no password on the account. |
| lastchg | Indicates the number of days between January 1, 1970, and the last password modification date. |
| min | Contains the minimum number of days required between password changes. |
| max | Contains the maximum number of days the password is valid before the user is prompted to specify a new password. |
| inactive | Contains the number of days a user account can be inactive before being locked. |
| expire | Contains the absolute date when the user account expires. Past this date, the user cannot log into the system. |

Some experienced system administrators will edit the /etc/passwd file directly for various reasons, but only after creating a backup copy of the original /etc/passwd file. In Chapter 18, “Name Services,” I describe this procedure. An example would be when you might want to restore an /etc/passwd file from backup—perhaps the original was corrupted or incorrectly modified. After modifying the /etc/passwd file, run the pwconv command. This command updates the /etc/shadow file with information from the /etc/passwd file.

> NOTE
Previous Solaris software releases used 32-bit data types to contain the UIDs and GIDs, but UIDs and GIDs were constrained to a maximum useful value of 60000. Starting with the Solaris 2.5.1 release and compatible versions, the limit on UID and GID values has been raised to the maximum value of a signed integer, or 2147483647. UIDs and GIDs over 60000 do not have full functionality and are incompatible with many Solaris features, so avoid using UIDs or GIDs greater than 60000.

> NOTE
Refrain from editing the /etc/passwd file directly, and never edit the /etc/shadow file directly. Any incorrect entry can prevent you from logging into the system. These files are updated automatically using one of the Solaris account administration commands, or Admintool, which are described in Chapter 5, “Setting Up User Accounts.”