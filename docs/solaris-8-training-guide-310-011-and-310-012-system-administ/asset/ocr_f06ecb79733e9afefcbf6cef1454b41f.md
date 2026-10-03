Several files that control default system access are stored in the /etc/default directory. These files limit access to specific systems on a network. Table 8.1 summarizes the files in the /etc/default directory.

# TABLE 8.1

# FILES IN THE /ETC/DEFAULT DIRECTORY

| Filename | Description |
|---|---|
| /etc/default/passwd | Controls default policy on password aging. |
| /etc/default/login | Controls system login policies, including root access. The default is to limit root access to the console. |
| /etc/default/su | Specifies where attempts to su to root are logged and where these log files are located. The file also specifies whether attempts to su to root are displayed on a named device (such as a system console). |

You can set default values in the /etc/default/passwd file to control user passwords. Table 8.2 lists the options that can be controlled through the /etc/default/passwd file.

# TABLE 8.2

# FLAGS IN /ETC/DEFAULT/PASSWD

| Flags | Description |
|---|---|
| MAXWEEKS | Specifies the maximum time period that a password is valid. |
| MINWEEKS | Specifies the minimum time period before the password can be changed. |
| PASSLENGTH | Specifies a minimum password length for all regular users. The value can be 6, 7, or 8. |
| WARNWEEKS | Specifies a time period warning of the password's ensuing expiration date. |