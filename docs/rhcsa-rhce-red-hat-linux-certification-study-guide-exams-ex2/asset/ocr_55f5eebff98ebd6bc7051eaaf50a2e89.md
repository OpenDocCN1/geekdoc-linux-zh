# SELinux Audits

Problems with SELinux should be documented in the associated log file, audit.log in the /var/log/audit directory. The file may be confusing, especially the first time you read it. A number of tools are available to help decipher this log.

First, the audit search (ausearch) command can help filter for specific types of problems. For example, the following command lists all SELinux events associated with the use of the sudo command:

```
# ausearch -m avc -c sudo
```

Such events are known as Access Vector Cache (-m avc) messages; the -c allows you to specify the name commonly used in the log, such as httpd or su. If you've experimented with the user_u SELinux user described earlier in this chapter, there should be several related messages available from the audit.log file.

Even for most administrators, the output is still a lot of gobblygook. However, it should include identifying information such as the audited user ID (shown as auid), which can help you identify the offending user. Perhaps the user needs such access, perhaps that user's account has been compromised. In any case, the alert may cause you to pay more attention to that account.

In contrast, the sealert -a /var/log/audit/audit.log command may provide more clarity. An excerpt is shown in Figure 4-12.

# SELinux Label and Context Issues

Considering Figure 4-12 and the SELinux concepts described so far, you might wonder if the user in question is allowed to run the sudo command. If the problem were in the /etc/sudoers file covered in Chapter 8, the SELinux alert message might not even appear. So you should pay attention to the source and target contexts. As they match, the file context is not the issue.

By process of elimination, that points to the user context described earlier as the problem. The UID of the user in question should be listed later in the file, under "Raw Audit Messages". If the user in question requires access to the sudo command, you should change the context of that user with the semanage login command described earlier. Otherwise, the user might just be experimenting with Linux. Any access to the sudo command will be documented in the /var/log/secure log file. So if that user actually gets by the SELinux-based limits on the use of the sudo command, it'll be documented in that file.