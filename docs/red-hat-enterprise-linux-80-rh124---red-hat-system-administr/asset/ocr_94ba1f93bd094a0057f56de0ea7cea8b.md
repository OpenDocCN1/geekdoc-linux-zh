# 2.4. Attempt to log in as operator1 again. This should succeed.

```
$student@servera ~$ su operator1
Password: redhat
...output omitted.
operator1@servera ~$
```

# 2.5. Exit out of the operator1 user's shell to return to the student user's shell.

```
$operator1@servera ~$ exit
logout
```

+   3. Change the password policy for operator1 to require a new password every 90 days. Confirm that the password age is successfully set.

# 3.1. Set the maximum age of the operator1 user's password to 90 days.

```
$student@servera ~$ sudo change -M 90 operator1
```

# 3.2. Verify that the operator1 user's password expires 90 days after it is changed.

```
$student@servera ~$ sudo change -l operator1
Last password change : Jan 25, 2019
Password expires : Apr 25, 2019
Password inactive : never
Account expires : never
Minimum number of days between password change : 0
Maximum number of days between password change : 90
Number of days of warning before password expires : 7
```

+   4. Force a password change on the first login for the operator1 account.

```
$student@servera ~$ sudo change -d 0 operator1
```

+   5. Log in as operator1 and change the password to forsooth123. After setting the password, return to the student user's shell.

# 5.1. Log in as operator1 and change the password to forsooth123 when prompted.

```
$student@servera ~$ su operator1
Password: redhat
You are required to change your password immediately (administrator enforced)
Current password: redhat
New password: forsooth123
Retype new password: forsooth123
...output omitted...
```