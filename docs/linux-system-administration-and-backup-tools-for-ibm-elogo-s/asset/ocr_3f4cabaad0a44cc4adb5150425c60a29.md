# USER ADMINISTRATION

In this dialog you can get information about existing users, create new users, and modify and delete existing users.

| User name | : |
| --- | : |
| Numerical user ID | : |
| Group (numeric or by name) | : |
| Home directory | : |
| Login shell | : |
| Password | : |
| Re-enter password | : |
| Access to modem permitted | [ ]

![](bbox=[0.166, 0.315, 0.813, 0.355])

Figure 91. YaST: user administration main window

Add a new user, fill in the blanks. The user name should be short and in lowercase (YaST) will do some verification on the (Input). If you pressed Tab or Enter to move to the next input field, YaST will automatically look for the next available user ID and assign it to this user. The entries Group, Home directory and Login shell will also be filled with default values, but you are free to change them to fit your requirements.

Some information about the different shells:

+   * /bin/bash - This is the Bourne Again Shell, which is an extension to the Bourne Shell. This is the most popular shell for Linux.
* /bin/sh - This is the standard Bourne Shell that has been around almost the entire reign of UNIX.
* /bin/ash - This is another version of the Bourne Shell.
* /bin/bsh - This is the same as /bin/sh to which it is linked.
* /bin/ksh - This is the standard Korn Shell that is the most popular shell for UNIX Administration.
* /bin/tcsh - This is a public domain extension of the C Shell.