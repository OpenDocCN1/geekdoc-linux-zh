You can then set up access to the SSH service with a line like the following in the /etc/hosts.allow file:

```
sshd : 192.168.122.50
```

While in most cases, the use of the fully qualified domain name for the noted IP address (server1.example.com) should work too, the use of the IP address is often appropriate. Limits by IP address don't depend on connections to DNS servers.

Of course, this is not the only way to limit access to the SSH to one system. It's possible within the /etc/hosts.deny file with a directive such as the following:

```
sshd : ALL EXCEPT 192.168.122.50
```

It's possible to set this up with other security options such as iptables command-based firewalls.

# Lab 6

Before this lab can work, however, you'll need to activate one SELinux boolean, ftp_home_dir. It's listed in the SELinux Management tool as "Allow ftp to read and write files in the user home directories." While this boolean setting is covered in Chapter 11, the basic management of SELinux, including the activation of boolean settings, is an RHCSA skill covered in Chapter 4. Therefore, with the key boolean identified, you should be able to set up vsFTP as described.

The description in this lab should point you to the /etc/pam.d/vsftpd configuration file. The model command line in this file is

```
auth required pam_listfile.so item=user sense=deny file=/etc/vsftpd/ftpusers
onerr=succeed
```

which points to the /etc/vsftpd/ftpusers file, a list of users to "deny" access. As the conditions in the lab suggest that you need a list of (one) user to which access is to be allowed, a second line of a similar type in this file is appropriate. To verify this lab, I included the following line:

```
auth required pam_listfile.so item=user sense=allow file=/etc/vsftpd/testusers
onerr=succeed
```

which allows all users listed in the /etc/vsftpd/testusers file. The onerr=succeed directive means that the vsFTP server still works if there's an error elsewhere in the line. For example, if there is no testusers file in the /etc/vsftpd directory, the directives in this line are forgiving, allowing the conditions for the auth module type to succeed.

As an experiment, try this lab with the boolean ftp_home_dir variable set and unset. That should demonstrate the power of SELinux and serve as an appropriate preview of Chapter 11.