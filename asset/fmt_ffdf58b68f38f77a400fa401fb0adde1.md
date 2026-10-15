
# OpenBSD: sshd_config, v 1.38 2001/04/15 21:41:29 deradt Exp $

# This sshd was compiled with PATH=/usr/bin:/usr/sbin:/sbin

# This is the sshd server system-wide configuration file. See sshd(8)

# for more information.

```
Port 22

#Protocol 2,1

#ListenAddress 0.0.0.0

#ListenAddress :

HostKey /etc/ssh/ssh_host_key

HostKey /etc/ssh/ssh_host_rsa_key

HostKey /etc/ssh/ssh_host_dsa_key

ServerKeyBits 768

LoginGraceTime 600

LoginRegenerationInterval 3600

PermitLogin yes

#

# Don't read ~/hosts and ~/.hosts files

IgnoreHosts yes

# Uncomment if you don't trust ~/.ssh/known_hosts

RhostsRSAAuthentication

#IgnoreUserKnown yes

StrictModes yes

X11Forwarding yes

X11DisplayplayOffset 10

PrintMotd yes

#PrintLog no

KeepAlive yes

# Logging

SyslogFacility AUTHPRIV

LogLevel INFO

#obsolete Mode and FascistLogging

RhostsAuthentication no

#

# For this to work you will also need need host keys in

/etc/ssh/ssh_known_hosts

RhostsRSAAuthentication no

# similar for protocol version 2
HostbasedAuthentication no
# RSAAuthentication yes

# To disable tunneled passwords, clear text passwords, change to no here!
PasswordAuthentication yes
PermitEmptyPasswords no

# To Uncomment to disable s/key passwords
#ChallengeResponseAuthentication no

# To Uncomment to enable PAM keyboard-interactive authentication
# Warning: enabling this may bypass the setting of
#PAMAuthenticationViaKdInt yes

# To change Kerberos options
#KerberosAuthentication no
#KerberosLocalPasswd yes
#AFTicketPassing no
#KerberosTicketCleanup

# Kerberos TGT Passing does only work with the AFS kaserver
#KerberosTgtPassing yes

#CheckMail yes
#UserLogin no

#MaxStartups 10:30:60
#Banner /etc/issue.net
#ReverseMappingCheck yes

| Subsystem | sftp | /usr/libexec/openssl/sftp-server |
```

以井号标记（`#`）开头的行是注释。注释解释了特定命令的用途。这些是被注释掉的命令。这些被注释掉的命令可以作为语法的示例。通过之前提供的命令列表，可以快速理解文件中参数的含义，但有两个值得注意的项。

首先，注意文件中包含多个 `HostKey` 语句。每行 `HostKey` 都指向不同的密钥，每个文件都包含一个适用于不同公钥加密协议的密钥。`ssh_host_rsa_key` 文件持有适用于 SSH 版本 1 的 RSA 密钥，而 `ssh_host_dsa_key` 文件持有适用于 SSH 版本 2 的 DSA 密钥。当在 Red Hat 系统上首次启动 `ssh` 时，这些 `HostKeys` 会为它们标识这些密钥。

```
[root]# service ssh start

Generating SSH1 RSA host key: [ OK ]

Generating SSH2 RSA host key: [ OK ]

Generating SSH2 DSA host key: [ OK ]

Starting sshd: [ OK ]
```
