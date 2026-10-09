+   The first field contains the account name. It must match the name found in /etc/passwd.

+   The second field contains the encrypted password. A * character here indicates that the account is disabled (that is, the user cannot log in), while a !! sequence here (followed by the original encrypted password) indicates that the account is temporarily locked.

+   The third field indicates the date when the password was last changed. It is expressed as the number of days elapsed since January 1, 1970. It is very typical, in systems of Unix descent, to count the number of days or seconds since this date. In the example above, we can see that eziodm's password was last changed 12100 days after January 1, 1970.

+   The fourth field contains a count of the number of days before the password *may* next be changed. The value zero or an empty field (as in the examples above) means that it can be changed anytime.

+   The fifth field contains a count of the number of days after which the password *must* be changed. This default value means that the password can stay in its place for almost 274 years, which is probably long enough!

+   The sixth field specifies how many days warning the user will get that their password is about to expire.

+   The seventh field specifies after how many days the account is disabled if its owner does not change the password when requested to.

+   The eighth field is the date when the account will be unconditionally disabled, expressed in days since January 1, 1970.

+   Finally, at the end of the line there is one more empty field, reserved for future use.

To get more information about `/etc/shadow`, you can consult its manual page, by typing `man 5 shadow` at your shell prompt.

# # Groups (the /etc/group File)

A user can belong to many groups, but as we've seen, `/etc/passwd` allows only membership of one group (the **primary group**). Membership of additional groups must be specified in the `/etc/groups` file. Unsurprisingly, this file is very similar in structure to the two we've already seen. The following example shows the groups we created earlier in this chapter:

```
root:x:0:root
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
eziodm:x:500:
kapis:x:501:
```