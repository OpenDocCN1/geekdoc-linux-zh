For example, to prevent joegunchy from logging in to the server from the 206.171.50.0 network, use the following line:

```
deny joegunchy 206.171.50.*
```

# /etc/ftpusers

The file /etc/ftpusers specifies the list of users who are not allowed to access the FTP server. The default /etc/ftpusers file contains the following users:

|  |  |
|---|---|
| root | halt |
| bin | mail |
| daemon | news |
| adm | uucp |
| lp | operator |
| sync | games |
| shutdown | nobody |

These accounts are not allowed to log in, because they are not real user accounts. If you need to stop a real user from being able to FTP to the server, put the username in this file.

At this point you have learned about all the configuration files necessary to run the FTP server. Now I will discuss some common FTP server configuration issues in the following sections.

![](bbox=[0.12, 0.9, 0.2, 0.98])

> **Tip**
> Because a lot of configuration is needed for proper FTP service, having a way to verify your configuration files periodically is useful. A utility called ftpck, which you can download from ftp://ftp.landfield.com/wu-ftpd/ftpck/, provides this type of periodic verification.

# Creating an anonymous FTP site

Having an anonymous FTP site can be a mixed blessing. It can be a great medium for distributing files that need to be widely distributed. In fact, all the free software packages (including the Red Hat Linux distribution) that you can download from the Internet are stored in many anonymous FTP