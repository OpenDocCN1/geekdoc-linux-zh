# Security

| Service | TCP/UDP Port number | Description | Red Hat Package | Security Level | Run it? |
|---|---|---|---|---|---|
| SMTP | 25 | Simple Mail Transfer Protocol. Used to transfer mail between systems. | sendmail | Weak. Mail transferred in plain text. | Only if mail needs to be handled locally. Encrypt sensitive mail before sending. |
| time | 37 | Sends current time (in seconds since 00:00 1st Jan 1900) back to sender. | xinetd | None. | No. Use NTP for time synchronisation. It is more accurate and has better security features. |
| finger | 79 | Gives information about local system or users to remote machine. | finger–server | None. | No. |
| http | 80 | Web server. | Httpd | Depends on server configuration. | Only if Web server needs to run on system. |
| auth (Ident) | 113 | Identification protocol. Allows remote system to determine identity of a user of a particular TCP/IP connection. | pident | Supports DES encryption of returned information. | Only if needed to access some public services (e.g. some ftp sites and IRC). |
| sftp | 115 | Secure File Transfer Protocol. FTP-like data transfers over secure SSH connection. | openssh | Good. | Only if file transfer required. |
| nntp | 119 | Network News Transfer Protocol. Used to transfer USENET news groups. | inn | Depends on server configuration. | Only if newsgroup server needs to be run on system. |

> Table continued on following page