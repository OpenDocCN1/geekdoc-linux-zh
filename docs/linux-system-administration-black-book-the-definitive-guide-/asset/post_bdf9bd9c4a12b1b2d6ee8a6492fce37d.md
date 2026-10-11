
## Immediate Solutions

### Securing FTP

To ensure that your FTP service with WU-FTP is as secure as possible, do the following:

1. Log in to the machine you want to secure as root.
   > NOTE: See Steps 1 through 5 of the section "Installing Anonymous FTP" to ensure that you have the user FTP server installed.
2. Type `vi /etc/ftpasscess` to open the file that regulates how **wu-ftpd** handles users.
3. Go to the following line:
   ```
   class all real,guest,anonymous *
   ```
4. This line creates a **class** of users named **all** that contains every type of FTP user possible. A **real** user is someone who has an account on your system. A **guest** logs in as "guest", and **anonymous** logs in as "anonymous". The difference between **guest** and **anonymous** is that a **guest** account is still an account. An /etc/passwd entry is involved, and a real password must be entered. Conversely, **anonymous** users log in as "anonymous" and typically use their email address as a password.
   If you want to add any additional classes, type "o" to open a new line below the current position and enter Insert mode, and add the new classes on the new blank line.
5. Continue down to the following line:
   ```
   email root@localhost
   ```
6. If you are currently in Insert mode, press the Esc key. Move the cursor to **root@localhost** and press "x" one character at a time to delete it. Then, press "i" to enter Insert mode and add an email address that points to the FTP administrator. For example:
   ```
   email ftpadmin@animals.org
   ```
7. Move down to:
   ```
   loginfails 5
   ```
8. This statement declares that if someone connects to your FTP server, he or she has five chances to enter a username and password correctly before the server hangs up. If you find that people are trying to break into your system, then lowering this value to 2 or 3 is a good idea. I cannot think of many reasons to raise the value, because legitimate users really should be able to enter their username and password correctly within five tries.
9. Continue to:
   ```
   readme  README*   login
   readme  README*   cwd=*
   ```
10. The first line notifies all users when they log in that the file README with any text attached to the end is available. The second line then ensures that if you change with the **cwd** command within an **ftp** session into a directory containing any files that begin with README, you are notified that the file exists.
    If you want any other files to be handled in this manner, add the appropriate **readme** statements below the current ones. Also, if you use different names for the documents containing this kind of information, edit the existing statements.
    > TIP: You can also comment out any line in this file by placing a hash mark (#) in front of it.
11. Proceed to the following pair of lines:
    ```
    message /welcome.msg  login
    message .message       cwd=*
    ```
12. In this case, the first line specifies that every user sees the contents of the file welcome.msg—stored in the base directory of the FTP file system space—as part of the text that displays when they log in. The second states that when the user changes into any directory in your FTP file system space that contains a file named .message, the contents of the .message file are displayed immediately.
    If you want or need to do so, do one of the following:
    - Comment out existing **message** statement(s) by putting a hash mark at the beginning of the line.
    - Edit the existing **message** statement(s) to suit your needs.
    - Add new **message** statements to suit your needs.
13. Cursor down to the following section:
    ```
    compress    yes    all
    tar        yes    all
    ```
14. These two lines act in concert. If an **ftp** user requests a group of files or an entire directory, having these two capabilities turned on tells the server to use the **tar** tool to bunch the directory together, and then to use the **compress** tool to make the resulting bundle smaller.
    Many administrators today shut off these features and instead offer pre-packaged file groupings for those who want them. The reason for doing this is that servers were getting overloaded constantly tarring and compressing data on the fly. If you want to do this, comment out the two lines with a hash mark, and then make sure to make tarballs of the various groups people might want.
15. Go down to the following set of lines:
    ```
    chmod    no    guest,anonymous
    delete   no    guest,anonymous
    overwrite  no   guest,anonymous
    rename   no    guest,anonymous
    ```
16. These lines set the FTP server such that anyone who is not a **real** FTP user cannot change file permissions, delete or rename a file, or replace it with another file. If you want to change one or more of these lines, or comment them out, do so.
17. Continue to this line:
    ```
    log transfers anonymous,real inbound,outbound
    ```
18. This line states that **wu-ftpd** should log both incoming and outgoing file transfers for all **real** and **anonymous** users. You can change this statement in a number of ways if you want to. If your primary concern is what is coming into your site from anonymous users, and you are low on file system space, then you might want to change this to the following:
    ```
    log transfers anonymous inbound
    ```
19. Cursor down to:
    ```
    shutdown /etc/shutmsg
    ```
20. If you do not intend to use this feature, comment the line out. If you do intend to use it, see the upcoming section “Creating A **shutdown** Message” for details on how to implement it properly. You can also change the file the message should go into, if you want to.
21. Finally, go to:
    ```
    passwd-check rfc822 warn
    ```
22. Leave this statement alone unless this machine only runs anonymous FTP service. If this is the case, change it to:
    ```
    passwd-check trivial enforce
    ```
    This action ensures that **wu-ftpd** looks for email addresses—or at least the @ symbol—in the passwords it receives and will not connect a user without that information. You can better track who is coming through when you ensure that you get email addresses as the password.
23. Press the Esc key to enter Command mode, and then type “ZZ” to save and close the file.
24. Type “vi /etc/ftphosts” to open the next file.
25. Type “G” to go to the end of the file, and then type “o” to open a new line at the end and enter Insert mode.
26. Add **allow** statements if you want them. These enable you to specify who can access your FTP site through specific usernames.
    > **WARNING!** *If you add any allow statements, it is assumed that you only want hosts that you define as allowed to be able to access your FTP site. You must explicitly allow everything you want to let in.*
27. Add **deny** statements if you want them. These enable you to specify particular locations from which people cannot access certain login names through FTP.
28. Press the Esc key to enter Command mode, and then type “ZZ” to save and close the file.
29. Type “vi /etc/ftpusers” to open the final FTP security file.
30. This file consists of a list of login names, one per line. Type “G” to go to the end, and then type “o” to open a new line beneath the list and enter Insert mode.
31. Add any usernames, one per line, that should not be allowed to log in through FTP.
32. Press the Esc key to enter Command mode.
33. Move the cursor to any usernames you want to allow to log in that are currently disallowed, and type “dd” to erase the line they are on.
    > **WARNING!** *Be very careful with this. The login names selected by default are there for security reasons.*
34. Type “ZZ” to save and close the file.
35. Type “/etc/rc.d/init.d/inet restart” to restart the superdaemon, which handles FTP service.

Related solution: Opening Or Creating Tarballs | Found on page: 110

### Installing Anonymous FTP

To install anonymous FTP service with the Red Hat Linux distribution (or one based on Red Hat), do the following:

1. Log in to the machine you want to secure as root.
2. If you do not already have the Red Hat CD-ROM in the CD-ROM drive, insert it.
3. Type “mount /mnt/cdrom” to mount the CD-ROM onto the file system.
4. Type “cd /mnt/cdrom/RedHat/RPMS” to change to the packages directory.
5. Type “rpm -q wu-ftpd” to see if you have this package installed already. If you do not, type “rpm -ivh wu-ftpd” and press Tab to complete the file name, and then press Enter to install the package.
6. Type “rpm -q anon-ftpd” to see if the anonymous FTP server is already installed. If it is, you are finished with this section.
7. If the anonymous FTP server isn’t installed, type “rpm -ivh anon-ftpd” and press Tab to complete the file name, and then press Enter to install it.
