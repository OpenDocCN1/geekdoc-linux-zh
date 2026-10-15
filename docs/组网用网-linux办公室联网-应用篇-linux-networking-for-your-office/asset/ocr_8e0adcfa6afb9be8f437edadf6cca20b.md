Samba options that affect name mangling and case-sensitivity include the following:

+   - **mangled names**—The default for this option is yes. If you set this option to no, Samba doesn't perform name mangling; it simply truncates filenames, which can result in two files having the same name. When this happens, you can access only one file.
+   - **mangle case**—Converts the case of files, normally providing all-uppercase names to the clients. The default is no.
+   - **case sensitive**—If this option is set to yes, Samba treats filenames in a case-sensitive manner. The default is no, which requires that Samba do more work to match filenames.
+   - **default case**—This option specifies the default case for new files from case-insensitive clients. The default is lower.
+   - **preserve case**—If this option is set to yes (the default), it preserves case from case-retentive OSs, such as Windows and OS/2. If it is set to no, filenames are converted to the default case.

# The Samba Daemons

Like most networking services, Samba operates by running daemons (p. 62). The Samba package contains two daemons:

+   - **smbd**—The SMB daemon provides the bulk of the services you think of when you think of Windows networking, including the all-important file-exchange services.
+   - **nmbd**—The name browser daemon is responsible for announcing the presence of your Linux server on the NetBIOS network. If it's not configured properly, you can't access your Linux computer's shares from Windows.

There are two ways to run the Samba daemons: independently and from inetd. Each has advantages and disadvantages.

# Running Samba Independently

If you type ps ax | grep mbd -, you get a report of services running that include the string mbd in their names. This includes both the Samba daemons, and normally not much else.

Here's some sample output from my system:

```
8243 ?  S  0:00 smbd -D
8254 ?  S  0:00 nmbd -D
```