# Network Information Service

Another aspect of account management under Enhanced Security is the Network Information Service (NIS). NIS is a distributed system used to centralize the management of a common set of system and network files, such as the password, group, and host files. NIS allows the system administrator to manage these shared files from a single server. NIS supports both Enhanced and Base Security on Digital and non-Digital machines. I do not manage any NIS systems, so I leave it as an exercise for the reader to determine the issues of implementing Enhanced Security in an NIS environment.

# Enhanced Security Logging

One unique feature of DU is a consolidated security authentication mechanism called the Security Integration Architecture (SIA). This SIA layer isolates the security-related commands (e.g., login, su, and passwd) from the specific security mechanisms that include, in addition to Base and Enhanced Security, optional products like

# Protected Password Authentication Database File Format — continued

u_succchg#828918424 This option specifies the time of the last successful password change. The time is specified as the number of seconds since the Epoch, 00:00:00 GMT 1 Jan 1970. Obviously, this time value is not immediately useful, and in fact, this field should only be set by programs (such as passwd(1)) that can be used to change the account password.

u_unsuccchg#8299276329 This option specifies the time of the last unsuccessful password change. This field should not be manually edited.

u_succlog#839193127 This option specifies the time of the last successful login. This field should not be manually edited.

u_suctty=tty1 This option specifies the name of the terminal associated with the last successful login to the account.

u_unsuclog#838691522 This option specifies the time of the last unsuccessful login. This field should not be manually edited.

u_unsuctty=tty1 This option specifies the name of the terminal associated with the last unsuccessful login to the account.

u_lock@ This Boolean option is used to administratively lock an account. A u_lock entry indicates that the account is locked; a u_lock@ entry indicates that it is not.

For additional information, see the manpage for prpasswd(4).