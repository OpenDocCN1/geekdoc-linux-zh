mainly as a security measure that aims to prevent possible brute force attacks targeted to obtain a user's account password.

With the `pam_faillock` module, failed login attempts are stored in a separate file for each user in the `/var/run/faillock` directory.

![](bbox=[0.08, 0.15, 0.16, 0.25])

# **NOTE**

The order of lines in the failed attempt log files is important. Any change in this order can lock all user accounts, including the **root** user account when the `even_deny_root` option is used.

Follow these steps to configure account locking:

+   1. To lock out any non-root user after three unsuccessful attempts and unlock that user after 10 minutes, add two lines to the `auth` section of the `/etc/pam.d/system-auth` and `/etc/pam.d/password-auth` files. After your edits, the entire `auth` section in both files should look like this:

```
```
1  auth       required      pam_env.so
2  auth       required      pam_faillock.so preauth silent audit
deny=3  unlock_time=600
3  auth       sufficient    pam_unix.so nullok try_first_pass
4  auth       [default=die] pam_faillock.so authfail audit deny=3
unlock_time=600
5  auth       requisite     pam_succeed_if.so uid >= 1000
quiet_success
6  auth       required      pam_deny.so
```
```

Lines number **2** and **4** have been added.

+   2. Add the following line to the `account` section of both files specified in the previous step:

```
```
account     required      pam_faillock.so
```
```

+   3. To apply account locking for the **root** user as well, add the `even_deny_root` option to the `pam_faillock` entries in the `/etc/pam.d/system-auth` and `/etc/pam.d/password-auth` files:

```
```
auth        required      pam_faillock.so preauth silent audit
deny=3 even_deny_root unlock_time=600
auth        sufficient    pam_unix.so nullok try_first_pass
auth        [default=die] pam_faillock.so authfail audit deny=3
even_deny_root unlock_time=600

account     required      pam_faillock.so
```
```

When user `john` attempts to log in for the fourth time after failing to log in three times previously, his account is locked upon the fourth attempt:

```
```
[yruseva@localhost ~]$ su - john
Account locked due to 3 failed logins
su: incorrect password
```
```