Variables you set are local to the current shell unless you mark them for export. Variables marked for export are called environment variables, and will be made available to any commands that the shell creates. The following command marks the variable BC for export:

```
export BC
```

You can list local variables by typing the set command. You can list variables that have been marked for export by typing the env command. The Bourne shell has several predefined variables, some of which are described in Table 12.4. These variables are assigned automatically when a user logs in, and are defined by the login program, the system initialization file, and the user's initialization files.

# TABLE 12.4

# DEFAULT BOURNE SHELL VARIABLES

| Variable | Description |
|---|---|
| ARCH | Sets the user's system architecture (for example, sun4, sun4c, sun4u). |
| CDPATH | Sets the search path for the cd command. |
| HOME | Sets the value of the user's home directory. |
| LANG | Sets the locale. |
| LOGNAME | Defines the name of the user currently logged in. The default value of LOGNAME is automatically set by the login program to the username specified in the /etc/passwd file. You should only need to reference (not reset) this variable. |
| LPDEST | Sets the user's default printer. |
| MAIL | If this parameter is set to the name of a mail file and the MAILPATH parameter is not set, the shell informs the user of the arrival of mail in the specified file. |
| MAILCHECK | Specifies how often (in seconds) the shell will check for the arrival of mail in the files specified by the MAILPATH or MAIL parameters. The default value is 600 seconds (10 minutes). If set to 0, the shell will check after each prompt. |
| MAILPATH | Sets the mail path by defining a colon-separated list of filenames. If this parameter is set, the shell informs the user of the arrival of mail in any of the specified files. Each filename can be followed by %, and a message that will be printed when the modification time changes. The default message is You have mail. |