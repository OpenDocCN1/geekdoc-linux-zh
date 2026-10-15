The default configuration in Figure 9.3 requires a user to change the password every eight weeks. The password must contain at least one alphabetic and one nonalphabetic character and each character can be repeated once. New passwords are checked against the dictionary file /usr/local/adm/pwdict/dictionary and verified using a locally developed loadable module in /usr/local/adm/checkpwd. Passwords cannot be reused within a year, and each new password must differ from the previous 25 passwords. Three days before a password expires, the user is reminded when logging on. Logins on Sundays are disabled.

Password history is enabled; the encoded password, with the time it was changed and the user ID to which it belonged, is stored in /etc/security/pwdhist.dir. Root owns this file and is the only user with read and write permissions.

# Logging

The files /etc/security/lastlog and /etc/security/failedlogin log failed login attempts per user. The record includes time and date, terminal, user ID, remote host, and number of unsuccessful attempts since the last successful login (see Chapter 8 for a detailed description of AIX v3 login configuration and tools to automate login surveillance). If the number of unsuccessful login attempts exceeds the loginretries value, the account is logged and a warning message is issued when the user tries to login.

/etc/security/portlog contains for each port the time a failed login occurred and the time a port was locked. Both are reset when the port is reenabled. The unsuccessful login times and occurrences are compared against the values of logininterval and logindisable to determine whether a port should be locked.

# Extending Password Verification

As I noted earlier, you can write your own extension to AIX v4's password verification functions. Extending the password verification requires you to write a C program, such as checkpwd.c (Listing 9.1) and to create a dynamically loadable object file [6]. Use the -e checkpwd option when you compile the sample code. This causes the compiler to use checkpwd() as the entry point instead of main().

You can use any function name other than main(). The login process uses the "load system" call to load the files listed in the pwdchecks attribute. The system call returns the address of the function specified with the -e option, and that function is then called. The function's return value indicates success (0) or failure (any other value). Memory for the returned error message must be allocated from the heap; the login process will free it.