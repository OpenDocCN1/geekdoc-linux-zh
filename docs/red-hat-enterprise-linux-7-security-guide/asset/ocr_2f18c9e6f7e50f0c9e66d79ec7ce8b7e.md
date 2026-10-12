```
```bash
~]# chmod 730 /var/ftp/pub/upload
```
```

A long format listing of the directory should look like this:

```
```bash
~]# ls -ld /var/ftp/pub/upload
drwx-wx---. 2 root ftp 4096 Nov 14 22:57 /var/ftp/pub/upload
```
```

Administrators who allow anonymous users to read and write in directories often find that their servers become a repository of stolen software.

Additionally, under `vsftpd`, add the following line to the `/etc/vsftpd/vsftpd.conf` file:

```
```text
anon_upload_enable=YES
```
```

# #### 4.3.9.3. User Accounts

Because FTP transmits unencrypted user names and passwords over insecure networks for authentication, it is a good idea to deny system users access to the server from their user accounts.

To disable all user accounts in `vsftpd`, add the following directive to `/etc/vsftpd/vsftpd.conf`:

```
```text
local_enable=NO
```
```

# ##### 4.3.9.3.1. Restricting User Accounts

To disable FTP access for specific accounts or specific groups of accounts, such as the root user and those with sudo privileges, the easiest way is to use a PAM list file as described in Section 4.2.1, “Disallowing Root Access”. The PAM configuration file for `vsftpd` is `/etc/pam.d/vsftpd`.

It is also possible to disable user accounts within each service directly.

To disable specific user accounts in `vsftpd`, add the user name to `/etc/vsftpd/ftpusers`

# #### 4.3.9.4. Use TCP Wrappers To Control Access

Use TCP Wrappers to control access to either FTP daemon as outlined in Section 4.4.1, “Securing Services With TCP Wrappers and xinetd”.

# ### 4.3.10. Securing Postfix

Postfix is a Mail Transfer Agent (MTA) that uses the Simple Mail Transfer Protocol (SMTP) to deliver electronic messages between other MTAs and to email clients or delivery agents. Although many MTAs are capable of encrypting traffic between one another, most do not, so sending email over any public networks is considered an inherently insecure form of communication. Postfix replaces Sendmail as the default MTA in Red Hat Enterprise Linux 7.

It is recommended that anyone planning to implement a Postfix server address the following issues.

# #### 4.3.10.1. Limiting a Denial of Service Attack

Because of the nature of email, a determined attacker can flood the server with mail fairly easily and cause a denial of service. The effectiveness of such attacks can be limited by setting limits of the directives in the `/etc/postfix/main.cf` file. You can change the value of the directives which are