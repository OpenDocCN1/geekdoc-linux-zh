| Effects | Does Not Affect |
| :--- | :--- |
| Prevents `root` access using the OpenSSH suite of tools. The following programs are prevented from accessing the `root` account:<br> • ssh<br> • scp<br> • sftp | Programs that are not part of the OpenSSH suite of tools. |

# Using PAM to limit root access to services

PAM, through the `/lib/security/pam_listfile.so` module, allows great flexibility in denying specific accounts. The administrator can use this module to reference a list of users who are not allowed to log in. To limit `root` access to a system service, edit the file for the target service in the `/etc/pam.d/` directory and make sure the `pam_listfile.so` module is required for authentication.

The following is an example of how the module is used for the `vsftpd` FTP server in the `/etc/pam.d/vsftpd` PAM configuration file (the `\` character at the end of the first line is not necessary if the directive is on a single line):

```
auth    required    /lib/security/pam_listfile.so    item=user \
sense=deny    file=/etc/vsftpd.ftpusers    onerr=succeed
```

This instructs PAM to consult the `/etc/vsftpd.ftpusers` file and deny access to the service for any listed user. The administrator can change the name of this file, and can keep separate lists for each service or use one central list to deny access to multiple services.

If the administrator wants to deny access to multiple services, a similar line can be added to the PAM configuration files, such as `/etc/pam.d/pop` and `/etc/pam.d/imap` for mail clients, or `/etc/pam.d/ssh` for SSH clients.

For more information about PAM, see *The Linux-PAM System Administrator's Guide* located in the `/usr/share/doc/pam-<version>/html/` directory.

Table 4.5. Disabling Root Using PAM