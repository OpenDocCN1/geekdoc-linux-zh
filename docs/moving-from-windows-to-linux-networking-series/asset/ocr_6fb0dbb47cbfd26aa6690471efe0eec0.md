# # WU-FTP

WU-FTP (Washingston University FTP Server) ships with Red Hat Linux 9.0. It is one of the most commonly used FTP servers in the world of Linux. If you followed the instructions in Chapter 2, it should be installed on your machine. You can check your packages, and if it is not installed, you can add it. Your first step in configuring this FTP server will be to find the configuration file. That can be found at `/etc/xinetd.d/wu-ftpd`. Change `disable = yes` to `disable = no`.

To change the permissions so that various users can access your FTP server, you will need to go to the access permission file found at `/etc/ftpaccess` directory. To allow a given user access you must make the following settings: `allow-uid ftp` (uid is the user ID) `allow-gid ftp` (gid is the group ID).

It is imperative that you make certain that users you have added match actual users on your system. Then make certain that the users' home directories are the ones where you want them to put their uploads. When you manage users and groups, you set each user's home directory. This will be the directory that he will first see when he connects with FTP. If you are using FTP to allow customers of a Web server to upload pages, then user `jdoe` would probably have a home directory something like `/var/www/html/users/jdoe/`.

The following entries in the configuration file are not critical, but it might be a good idea to take a look at them:

+   - `readme`: This setting in the `config` file identifies a readme file that users have access to.
+   - `e-mail root@localhost`: This is the admin's e-mail address.
+   - `loginfails 5`: How many login attempts before failure?
+   - `message`: This is the welcome message file you want to display.

Now you can start WU-FTP by typing `>/etc/init.d/xinetd restart` at the shell. To stop the FTP server, type `ftpshtut now`.

The configuration you have just seen is very basic. You would be well advised to spend some time reading the documentation on the WU-FTP Web site.

As a final word of caution, you should bear in mind what was stated at the beginning of this chapter. FTP servers can be a significant security risk. If this chapter is your first introduction to FTP servers, then you are advised to not set one up on a commercial or business server without first reviewing all of the documentation for that Web server. Go to that Web server's home page and read the online documentation, with particular attention to the security notes.