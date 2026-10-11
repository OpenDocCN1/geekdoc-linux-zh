
minimum. If you have no serial devices attached to the system and you are not using virtual consoles, the only entry in `/etc/security` should be `tty1`. We discourage this approach generally and particularly on systems that are important (as defined by your Security Policy) because, while native logins are logged, you will neither be able to track the original user who logged in as root nor can you restrict access as root to certain users when they log in on the allowable device(s) specified in `/etc/security`.

**Secure User and Group Accounts**

There are a couple of ways to manage your user and group accounts, manually or through a service such as NIS. If you are managing them manually, use the shadow file as described in Password Aging and the Shadow File on page 61. You can either add the necessary users one at a time or copy, via `scp` (of course—see Chapter 11), the `/etc/passwd` and `/etc/shadow` files from another system. Be sure to review these files for correctness before going on. The same comments apply for group accounts. If you use NIS or NIS+ or a similar service, configure your system for that purpose. Note that, as of this writing, NIS cannot use shadow files and opens a variety of other vulnerabilities. See NFS, Samba, NIS, and DNS Resources on page 40 for further details. In any event, be thoroughly familiar with the service you are using to maintain your user and group accounts before you implement it.

**Configure PAM and OTP**

PAM is discussed in Chapter 5 and OTP (OPIE and S/Key) are discussed in Chapter 6.

As noted in Install Your System on page 517, make sure you configure PAM with MD5 password hashing. Also, be sure to set `minlen` reasonably large (see PAM and Passwords on page 86). Your Security Policy should dictate the size, but, in the absence of a policy, we recommend a minimum length of 16 characters and encourage the use of passphrases requiring at least one of each different type of character.

There are a great many features with PAM, so take advantage of them in accordance with your Security Policy. In particular, you will probably want to enforce login times (`pam_time`), resource limits (`pam_limits`), and access control lists (`pam_listfile` or `pam_access`) on critical systems.

It is probably too inconvenient to implement OPIE everywhere, but it is a good idea to minimally implement it on any critical servers in your environment. We strongly recommend the use of OPIE on all systems exposed to your external network (Internet or other untrusted network). In particular, your firewall and DMZ systems (see Firewalls and the DMZ on page 525) should be configured to authenticate exclusively with OPIE.

**Configure syslog, logrotate, logcheck, and swatch**

Configuring syslog is discussed in Chapter 8. Implementing and configuring logrotate, logcheck, and swatch are discussed in Chapter 17. We will refer to these tools as log management tools. Throughout the book we discussed configuring log management for a variety of circumstances.

You want to configure **syslog** and the log management tools to meet the needs of your environment. Certain systems will need to be configured in different ways; for example, a web server will need to have additional configuration for the log management tools to capture the essential information it generates. All critical systems in your environment should be configured to write log messages locally **and** to a central log host. The central log host should be treated as a critical system and allow a minimum of services (ideally only SSH). It should also allow only administrator (users who are the administrators) access.

If you are going through the process of log file management for the first time, or you have limited experience with it, take a dynamic approach. Pay close attention to the messages generated and decide which entries need your attention and which do not. Initially, err on the side of too much information. As you become more comfortable with the log entries, you will be able to filter out those that are not important.

The goal is to have your utilities generate as many log entries as are necessary to meet your Security Policy. In some cases, this will mean that you must maintain an audit trail of all activity on some systems. For systems that require it, turn on process accounting and include its logs as well as connection accounting (log your review process, see Chapter 7). You may also need to run **auditd** (see *The auditd Utility* on page 171) on some or all of your systems. The goal for the **logcheck** and **swatch** utilities is to capture critical information and make you aware of it quickly so that you can attend to the problem and deal with it appropriately. Have all of the messages sent to a central e-mail address that gets read regularly.

The rest of the log data is to be maintained by **logrotate**. It is a good idea to archive your log files in their entirety for some period of time (check your Security Policy, but 1 to 3 years is not uncommon). Be sure to add the appropriate and necessary *prerotate* and *postrotate* scripts (see *logrotate* on page 492).

## Configure **sudo**

The **sudo** utility is covered in Chapter 9. When preparing *sudo* for compilation with the configure utility, choose the appropriate options. We recommend that you minimally use `--with-pam` and `--with-ignore-dot` (and, of course, `--with-insults`). Once you have compiled *sudo*, you may make it available to other systems employing the same architecture type (for example, x86).

Set up your `/etc/sudoers` file so that it is as simple as possible and grants the minimum necessary privileges. Recall that the configuration file is configurable for many hosts, or depending on your environment you may need only one file. If you prefer, you may configure `/etc/sudoers` for each "class" of host. A class of hosts would be, for example, the collection of all desktops used in an engineering group. Another class might be the collection of NFS servers maintained by the same group of administrators. Either way, keep it simple and limit privileges.

The most secure way of implementing sudo is with OTP (see Chapter 6). The most flexible way of doing this is through PAM (see PAM and sudo on page 189) and OPIE (see OPIE and PAM on page 143). It is not as inconvenient as it first seems, and after all only the administrators need to do this. So it's not like you are asking all of your users to use OTP. Minimally implement OPIE on your critical servers.

## Configure Network Services

Network services, TCP_wrappers, the portmap daemon, and xinetd are discussed in Chapter 10. Minimally, make sure that all of the r-commands (see Trusted Host Files and Related Commands on page 36) are disabled. Use SSH (see Implement and Configure SSH below) if you require that functionality.

The really great news is that Red Hat 5.2/6.0 incorporates TCP_wrappers for all services invoked through inetd. Take advantage of this. Since we are assuming that which is not expressly permitted is forbidden, create `/etc/hosts.allow` to contain the allowable services and hosts. The `/etc/hosts.deny` file must minimally contain `ALL:ALL` (to deny everything that is not explicitly allowed) and, based on your Security Policy, may contain boot traps and additional logging rules (as described in Access Control with TCP Wrappers on page 202) to capture information about unauthorized attempted access. Make sure that you include the necessary portmap restrictions as well (see Implementing Portmap Access Control on page 223). If a service is not permitted and your Security Policy does not require logging of attempted use of those services, then make sure to comment out `/etc/inetd.conf`.

Someday, perhaps, xinetd will be distributed with Linux instead of inetd. Such a distribution would be fantastic. For now, however, replacing inetd with xinetd on all of your systems may be too tedious. If you adopt the concepts put forth in Reducing the Workload on page 523, you will be able to considerably reduce the effort associated with implementing xinetd everywhere. Unfortunately, there is a fair amount of work up front to reach that point. Thus, we strongly recommend that you minimally implement xinetd on all critical servers and all systems exposed to the external network (see Firewalls and the DMZ on page 525). Take full advantage of the process limitations and log file size limitations (see Replacing inetd with xinetd on page 226) that may be imposed by xinetd. Also, use TCP_wrappers for all services with xinetd, just as you would for inetd in conjunction with the other access control capabilities, such as `bind`, `access_times`, `only_from`, and `no_access` (see Table 10.10 on page 232).

## Implement and Configure SSH

You must use SSH (or something similar, such as SSLeay; see Secure Shell Alternatives on page 310) for all remote root access. Period. See Chapter 11 for the details of SSH. We strongly recommend that you implement and use SSH for all X Window System access (see Exploring ssh Functionality on page 304). While this will not prevent theft of `.xauth` files or similar credentials...
