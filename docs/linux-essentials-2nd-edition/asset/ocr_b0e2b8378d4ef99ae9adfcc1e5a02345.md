# Chapter 12 · Understanding Basic Security

Days of Warning Before Password Expiration If your system is configured to expire passwords, you may set it to warn the user when an expiration date is approaching. A value of 7 is typical. However 14 days, as shown in the preceding example, may be appropriate if your company's employees take two-week vacations.

Days Between Expiration and Deactivation Linux allows for a gap between the expiration of an account and its complete deactivation. An expired account either cannot be used or requires that the user change the password immediately after logging in. In either case, its password remains intact. A deactivated account's password is erased, and the account cannot be used until the system administrator reactivates it. A -1 in this field, as shown in the preceding example, indicates that this feature is disabled.

Expiration Date This field shows the date on which the account will expire. As with the last password change date, the date is expressed as the number of days since January 1, 1970. A -1 in this field, as shown in the preceding example, indicates that this feature is disabled.

The terms encrypted and hashed are often confused when used with computer objects. You can decrypt an encrypted object, but you cannot "dehash" a hashed object. Passwords on Linux are salted and hashed, though you'll often see the term mistakenly used instead in Linux documentation.

Special Flag This field is reserved for future use and normally isn't used or contains a meaningless value. This field is empty in the preceding example.

For fields relating to counting days, a value of -1 or 9999 typically indicates that the relevant feature has been disabled. The /etc/shadow values are generally best left to modification by commands such as usermod (described in Chapter 13) and change. Understanding format of files enables you to review its contents and note any discrepancies, which could indicate that your system has been compromised.

Examples of user files stored outside the user's home directory include email in /var/spool/mail/ and temporary files in /tmp.

The /etc/shadow file is usually stored with restrictive permissions, by root. This is craft to the shadow password system's utility because it keeps non-root users from reading the file and obtaining the password list, even in a salted and hashed format. By contrast, /etc/passwd must be readable by ordinary users and usually has less-restrictive permissions.

It's important to realize that an account is not a single entity like a binary file. Account information is scattered across several configuration files, such as /etc/passwd, /etc/shadow, /etc/group, and possibly in other configuration files User reside in the users home directory and perhaps elsewhere. Managing accounts can require doing more than just maintaining a file. For this reason, various utilities exist to help create, manage, and delete accounts, as described in the rest of this chapter and in Chapter 13.

*