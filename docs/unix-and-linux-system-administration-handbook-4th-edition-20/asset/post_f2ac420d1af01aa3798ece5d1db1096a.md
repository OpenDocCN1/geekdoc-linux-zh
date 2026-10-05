
# A detailed Linux configuration example

Let’s look at the specific modules.

The pam_authtok_get library routine prompts the user for a login name (if one has not already been set) and password and stores these values in the token called PAM_AUTHTOK. The pam_dhkeys module is used for RPC (re-procedure call) authentication for NIS or NIS+ and is looking for Diffie-Hellman keys, hence the name.

The pam_unix_cred module sets the credentials for the authenticated user, and the pam_unix_auth module performs the actual authentication, checking the value stored in PAM_AUTHTOK is the user’s correct password. Finally, the module pam_dial_auth authenticates the user for dialup access according to the contents of /etc/dialups and /etc/d_passwd.

You may see the same module referred to more than once in a configuration file, with different module-type values. That’s fine; multiple type implementations are often collected into a single library if they share significant code.

# A detailed Linux configuration example

Linux moves each set of PAM configuration lines that refer to the same service into a separate file after that. The format is the same except that the service field is no longer needed.

For example, the /etc/pam.d/login file from a SUSE system is reproduced with the included expanded to form a more coherent example.

```
auth requisite pam_nologin.so
auth requisite [user_unknown]ignore success=ok ignore=ignore auth_err=die
      default=bad] pam_security.so
auth required pam_env.so
auth required pam_unix2.so
account required pam_unix2.so
password requisite pam_pwck.so null cracklib
password required pam_unix2.so use_authtok null
session required pam_loginuid.so
session required pam_limits.so
session required pam_unix2.so
session optional pam_umask.so
session optional required pam_lastlog.so nowtmp
session optional pam_mail.so standard
session optional pam_ck_connector.so
```

The auth stack includes several modules. On the first line, the pam_nologin module checks for the existence of the /etc/nologin file. If it exists, the module aborts the login immediately unless the user is root. The pam_secure module ensures that root can only log in on terminals listed in /etc/security. This line uses the alternative Linux syntax described in the pam.conf page. In this case, the requested behavior is similar to that of the required control flag. pam_env sets environment variables from /etc/security/pam_env.conf, and 

# Chapter 22

# Security

finally, pam_unix2 checks the user's credentials by performing standard UNIX authentication. If any of these modules fail, the auth stack returns an error.

The account stack includes only the pam_unix2 module, which in this context assesses the validity of the account itself. If it returns an error, if for example, the account has expired or the password must be changed. In the latter case, the module collects a new password from the user and passes it to the password modules.

The pam_pwcheck library checks the strength of proposed new passwords by calling the cracklib library. It returns an error if the new password does not meet the requirements. However, it also allows empty passwords because of the nullok flag. The pam_unix2 updates the actual password.

Finally, the session modules perform several housekeeping chores. pam_login sets the kernel's login attribute to the user's UID. pam_limits reads resource limits from /etc/security/limits.conf and sets the corresponding process parameters that enforce them. pam_umask sets the user's access to the system, and pam_lastlog module displays the user's last login time as a security check, and the pam_mail module prints a note if the user has new mail. pam_ck_connector notifies the ConsoleKit daemon (a system-wide daemon that manages login sessions) of the new.

At the end of the process, the user has been successfully authenticated and PAM returns control to login.

# 22.6 SETUID PROGRAMS

Setuid programs (executables on which the setuid bit has set) run as the user who owns the executable file. For example, the password program must run as root to modify the /etc/shadow file when users change their passwords. Setuid and setgid execution on page 106 for basic information about this feature.

Programs that run setuid, especially ones that run setuid to root, are prone to security problems. The setuid commands distributed with the system are theoretically secure; however, security holes have been discovered in the past and will undoubtedly be discovered in the future.

The surely way to minimize the number of setuid problems is to minimize the number of setuid programs. Think twice before installing software that needs to run setuid, and avoid using the setuid facility in your home-grown software. Never use setuid execution on programs that were not explicitly written with setuid in mind.

You can disable setuid and setgid execution on individual filesystems by specifying the nosuid option to mount. It's a good idea to use this option on filesystems that contain users' home directories or are mounted from less trustworthy domains.

# Effective use of chroot

It's useful to scan your disks periodically to look for new setutid programs. A hacker who has breached the security of your system sometimes creates a create setuid shell or utility to facilitate repeat visits. Some of the tools discussed starting page 914 locate such files, but you can do just as well with **find**. For example, the one-liner script below

```
/usr/bin/find / -user root -perm -4000 -print | \
/bin/mail -s "Setuid root files" netadmin
```

mails a list of all files that are setuid to root to the “netadmin” user. (In practice, you may need to be more specific about which filesystems to search.)

# 22.7 EFFECT USE OF CHROOT

The **chroot** system call confines a process to a specific directory. It disallows access to files outside or above that directory thereby limits the damage the process can cause if it should be compromised by a hacker.

The **chroot** command is a simple wrapper around this system call. In addition, some security-sensitive daemons have **chroot** support built in and need only this mode turned on in their configuration files.

Security experts sometimes frown upon use of **chroot** for security purposes because they believe that when it is poorly or misused, it can give administrators a false sense of security. They complain that some administrators use **chroot** to excuse themselves from other forms of security diligence as regular software updates and close security monitoring.

These points are not inaccurate, but they're not the last word on **chroot**, either. Similar claims could be made regarding network firewalls, but few experts would recommend using the packet filter from your network. Used correctly as a supplemental layer of protection, **chroot** is a worthy addition to your security arsenal (even if that was not the feature's original design intent).

The following scenarios illustrate reasonable uses of **chroot**:

- Want to run a non-daemon process such as Apache or BIND within a restricted filesystem subtree. If the daemon is compromised, the attacker will be restricted to the subtree as long as no privilege escalation vulnerabilities exist.
- Want to restrict remote users to a specific set of files and commands.

However, **chroot** can only protect you in these scenarios if all of the following conditions are met:

- All processes in the **chroot** jail without root privileges. Processes that run as root always have the ability to break out of the **chroot** jail.
- You are not using setuid root execution within the jail.
- The chroot environment is up to date and minimal, in the sense that it contains only the executables, libraries, and configuration files that are needed to support the intended task. In this era of shared libraries and interprocess dependencies, constructing a proper jail can be tricky. JailKit (olivier.sessink.nl/jailkit) includes several scripts to help you create ch environments.

# Chapter 22 Security

# 22.8 SECURITY POWER TOOLS

Some of the time-consuming chores mentioned in the previous sections can be automated with freely available tools. Here are a few of the tools you'll want to look at.

# Nmap: network port scanner

Nmap is a network port scanner. Its main function is to check a set of target hosts to see which TCP and UDP ports have listening on them. Since most network services are associated with “well known” port numbers, this information tells you quite a lot about the software machine is running.

Running Nmap is a great way to find out what a system looks like someone on the outside is trying to break. For example, here's a report from a production Ubuntu system:

```
ubuntu nmap -sT ubuntu.booklab.atrust.com
Starting Nmap 4.20 (http://insecure.org ) on 2009-11-01 12:31 MST
Interesting ports on ubuntu.booklab.atrust.com (192.168.0.25):
Not shown: 1691 closed ports
PORT STATE SERVICE
25/tcp open smtp
80/tcp open http
111/tcp open rpcbind
139/tcp open netbios-ssn
445/tcp open microsoft-ds
3306/tcp open mysql
```

Nmap finished: 1 IP address (1 host) scanned in 0.186 seconds
By default, nmap includes the -sT argument to try to connect to each TCP port on the target host in the normal way. Once a connection has been established, nmap immediately disconnects, it is impolite but not harmful to a properly written network server.

- 3. As described in Chapter 14, a port is a numbered communication channel. An IP address identifies an entire machine, and an IP address + port number identifies a specific server or network conversation on that machine.
- 4. Actually, the privileged ports (with port numbers under 1024) and the well-known ports are checked by default. Use the -p option to explicitly specify the range of ports to scan.
