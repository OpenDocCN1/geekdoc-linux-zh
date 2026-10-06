# 118 Part I: Hacking Techniques and Defenses

pass wrongpassword
530 Login incorrect.
CWD ~
530 Please login with USER and PASS.
Connection closed by foreign host.

```
[bash]$ strings /core | grep root
root:$1PykBWI83bckLZ7CbBsPhXUCHlnoql:12241:0:99999:7::
```

Once an intruder has access to the password hash of the root user, he or may use a tool such as John the Ripper to force-crack the password. Please see **securityfocus.com/bid/261** for more information about this Solaris FTP server vulnerability. See Chapter 4 for more details on how to perform password cracking using John the Ripper.

![](bbox=[0.088, 0.335, 0.122, 0.368])

# Promptly Install Software Patches

Software vendors often release patches to announced vulnerabilities. Make sure to install such patches before the vulnerabilities are exploited by malicious users.

# Misconfigurations

Frequently, administrators focus all their attention on hardening remote services. Negligence toward local services and applications may lead to various misconfigurations that allow local users to obtain higher privileges. For example, an administrator may purposely configure a database server running on the host to allow any user to connect with no password. Although a firewall prevents remote users from logging in to the database server, such a configuration may easily allow a local user to elevate privileges. Therefore, routine hardening and auditing of the configurations of local services and applications is strongly advised.

# SUMMARY

This chapter focused on techniques used by intruders to elevate their privileges to those of the root user. You learned of the dangers of trusting local users, improper file permissions, misconfigurations, and softwarevulnerabilities. After an intruder obtains root permissions, he or will have total control of the victim next. The intruder must hide his or her tracks, and plant Trojans and backdoors in order to ensure continued access. These topics are discussed in the following chapter.

Remember to see Part II of this book for information on how to perform host hardening, which will help protect against many of the privilege escalation attacks presented in this chapter.