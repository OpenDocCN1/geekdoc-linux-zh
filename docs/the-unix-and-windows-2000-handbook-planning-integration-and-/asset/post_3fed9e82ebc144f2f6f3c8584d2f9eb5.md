
running in the domain. Passwords must not be changed on the UNIX systems. This type of system can work well in an environment in which UNIX systems are utilized as backend servers with no interactive sessions for the unwashed (non-system administrators). Let's go through the procedure for setting up this service.

The first thing you will need to do is purchase the required number of licenses from Microsoft to run the services on all of your Windows 2000 domain controllers. Next you will need to configure your UNIX hosts that will be doing the synchronization. You have a choice of sending the password in clear or encrypted text. Root must be able to do an rlogin to the UNIX host for a clear text password. The encrypted text version requires FTPing the ssod daemon and ssod.config files to the same directory on the UNIX host. You must then modify the ssod.config file. The PASSWORD variable is the encryption key that must be at least 12 characters long and contain characters from at least three of the groups in Table 7.6. You will need this encryption key when you set up the service on your Windows 2000 servers. After modifying the ssod.config file, you will need to start the SSOD daemon as root. Problems with the daemon will be reported on the system console or in the syslog file (depends on how your /etc/syslog.conf file is configured on the UNIX workstation). Automatically starting the services will require a simple shell script addition to the appropriate directory in the boot process (see Chapter 3, "System Boot and Shutdown").

Now that the UNIX workstation is ready and running, we need to install the software on all of the Windows 2000 domain controllers. Once it is installed, enter the following:

```
Start->Programs->Windows NT Services for UNIX->Password Synchronization (Common)->Password Synchronization Administrator
```

You will then be presented with the screen shown in Figure 7.31 and should follow these steps:

| Table 7.6 Encryption Character Groups |  |
|---|---|
| Group | Characters |
| 1 | A, B, C, ... Z |
| 2 | a, b, c, ... z |
| 3 | 0, 1, 2, ... 9 |
| 4 | (~!@#$%^&*_+=[]\|;:",<> .?) |

![](img/415c89a1ede71e11e5040a0038b6916c_315_0.png)

## Figure 7.31

- 1. Click the Add button and you will be presented with the screen shown in Figure 7.32.
- 2. Type a meaningful name and click OK. The next screen (Figure 7.33) will require the configuration information that was previously completed for the UNIX workstation.
- 3. First select clear (Use Rlogin) or encrypted (Use encryption) text. If you are using encryption then you will need to click the Configure button and enter the encryption key you entered on the UNIX host.
- 4. Next you will need to add all the IP addresses of the fully-qualified domain names of the UNIX hosts configured to do synchronization with Windows 2000. Initially check Enable verbose logging; this will greatly enhance your ability to debug any problems that may arise.

![](img/415c89a1ede71e11e5040a0038b6916c_315_1.png)

## Figure 7.32

![](img/415c89a1ede71e11e5040a0038b6916c_316_0.png)

Figure 7.33

- 5. You can exclude accounts from being synchronized. Create a group in Windows 2000 called PasswordPropDeny. Add all user accounts to this group that should be excluded from the password synchronization process.
- 6. Finally, you will need to change the password on a test account and check the Event Viewer and logs on the UNIX workstation to ensure passwords are being changed in the UNIX domain.

> Beware of typos in the encryption key.

## Lightweight Directory Access Protocol

Where do you go to find information on your users? How do you keep your accounts and passwords synchronized? Can you even locate all of the different databases you maintain in your UNIX and Windows 2000 worlds? Does adding a new user require updating multiple databases on Windows and UNIX systems? Is it a nightmare to delete accounts?

What you really want is a centralized database that allows you to enter information once about a new user. This new user would have a Windows 2000 account, a UNIX account, a single password, group privileges, email account, and be a member of all required mailing lists for the organization. The new user should also be included in the company's phone book and organizational charts. This database would also allow you to remove users from all of the above with just one simple action. Additionally this database
