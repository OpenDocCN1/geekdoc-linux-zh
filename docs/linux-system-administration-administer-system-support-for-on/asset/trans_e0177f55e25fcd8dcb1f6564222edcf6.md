
```text
Welcome to Linux 2.0.33.
tigerden login:
127.0.0.1: -- telnetd end output --
# Time Stamp(13924): Telnetd linker check: (899851239) Tue Jul  7 15:40:39
127.0.0.1: -- dynamic linker environment begin test --
Welcome to Linux 2.0.33.
tigerden login:
127.0.0.1: -- dynamic linker environment end test --
# Time Stamp(13924): X11 Display check: (899851249) Tue Jul  7 15:40:49
# Trying to Open Display 127.0.0.1:0
127.0.0.1: X Display Opened
# Time Stamp(13924): Finger check: (899851249) Tue Jul  7 15:40:49
# Checking Finger on port 79
# Time Stamp(13924): RTM finger check: (899851249) Tue Jul  7 15:40:49
# Time Stamp(13924): SMTP check: (899851250) Tue Jul  7 15:40:50
# Time Stamp(13924): Imapd buffer overflow: (899851250) Tue Jul  7 15:40:50
# 127.0.0.1 imapd/pop B0 could not connect 107
#127.0.0.1:  -imapd/pop B0 could not connect 107
# The following  is output from Sendmail port.  If the output contains lines
# like "/usr/bin/uudecode", "Please pass, oh mighty wizard", and
# "200 Debug set", please read the manual to fix these vulnerabilities.
#   If "250 <decode>" and "250 <uudecode>" are output, then VRFY is not
# implemented and the aliases on the machine need to be checked internally.
127.0.0.1: -- SMTP version begin output --
220 tigerden ESMTP Sendmail 8.8/8.8.8; Tue, 7 Jul 1998 15:40:55 -0700
127.0.0.1: -- SMTP version end output --
```

对于检查主机安全性，TAMU Tiger 和 Crack 是非常棒的工具。TAMU Tiger 承接了 COPS 未完成的工作。Tiger 允许你对你的主机进行深度扫描，包括路径和其他可能的密码文件。

**Listing 2-4** 展示了 Tiger 系统扫描的结果。这展示了重要的信息，如全球可读的文件和目录，root 路径中的文件，以及服务文件。

### **Listing 2-4**：Tiger 系统扫描结果

```text
Security scripts *** 2.2.3, 1994.0309.2038 ***
Thu Jun  4 09:28:41 PDT 1998
09:28> Beginning security report for mymachine (i586 Linux 2.0.30).

# Performing check of passwd files...

# Performing check of group files...

# Performing check of user accounts...
# Checking accounts from /etc/passwd. 
 --WARN- [acc006w] Login ID ftp's home directory (/home/ftp) has group 'wheel' write access. 
 --WARN- [acc006w] Login ID lp's home directory (/var/spool/lpd) has group 'lp' write access. 
 --WARN- [acc006w] Login ID mail's home directory (/var/spool/mail) has group 'mail' write access. 
 --WARN- [acc006w] Login ID postmaster's home directory (/var/spool/mail) has group 'mail' write access. 
 --WARN- [acc006w] Login ID uucp's home directory (/var/spool/uucppublic) has group 'uucp' and world write access.
```

```text
# Performing check of /etc/hosts.equiv and .rhosts files... 
 --WARN- [rcmd013w] /etc/hosts.equiv contains an attempted comment line 
 --WARN- [rcmd013w] /etc/hosts.equiv contains an attempted comment line 
 --WARN- [rcmd013w] /etc/hosts.equiv contains an attempted comment line 
 --WARN- [rcmd013w] /etc/hosts.equiv contains an attempted comment line 
 --WARN- [rcmd013w] /etc/hosts.equiv contains an attempted comment line 
 --WARN- [rcmd013w] /etc/hosts.equiv contains an attempted comment line 
 --WARN- [rcmd013w] /etc/hosts.equiv contains an attempted comment line 
 --WARN- [rcmd013w] /etc/hosts.equiv contains an attempted comment line 
 --WARN- [rcmd013w] /etc/hosts.equiv contains an attempted comment line 
 --WARN- [rcmd013w] /etc/hosts.equiv contains an attempted comment line 
 --INFO- [rcmd010i] /etc/hosts.equiv contents: 
 # 
 # hosts.lpd This file describes the names of the hosts which are 
 # to be considered "equivalent", i.e. which are to be 
 # trusted enough for allowing rsh(1) commands. 
 # 
 # Version: @(#)/etc/hosts.lpd 2.00 04/30/93 
 # 
 # Author: Fred N. van Kempen, <waltje@uawalt.nl.mugnet.org 
 #
```

```text
localhost 
 # End of hosts.lpd. 
 
 # Checking accounts from /etc/passwd... 
 
 # Performing check of .netrc files... 
 
 # Checking accounts from /etc/passwd...
```

```text
# Performing check of PATH components...
# Only checking user 'root'
--WARN-- [path002w] /usr/bin/nm in root's PATH from default is not owned by root (owned by news).
--WARN-- [path002w] /usr/bin/nmadm in root's PATH from default is not owned by root (owned by news).
--WARN-- [path002w] /usr/bin/nmbatch in root's PATH from default is not owned by root (owned by news).
--WARN-- [path002w] /usr/bin/nmcheck in root's PATH from default is not owned by root (owned by news).
--WARN-- [path002w] /usr/bin/nmjoback in root's PATH from default is not owned by root (owned by news).
--WARN-- [path002w] /usr/bin/nmgrab in root's PATH from default is not owned by root (owned by news).
--WARN-- [path002w] /usr/bin/nmgrq in root's PATH from default is not owned by root (owned by news).
--WARN-- [path002w] /usr/bin/nmprint in root's PATH from default is not owned by root (owned by news).
--WARN-- [path002w] /usr/bin/nmprintjob in root's PATH from default is not owned by root (owned by news).
--WARN-- [path002w] /usr/bin/nmstat in root's PATH from default is not owned by root (owned by news).
--WARN-- [path002w] /usr/bin/nmutil in root's PATH from default is not owned by root (owned by news).
--WARN-- [path002w] /usr/bin/nmusage in root's PATH from default is not owned by root (owned by news).
--WARN-- [path002w] /usr/sbin/edquota in root's PATH from default is not owned by root (owned by bin).
--WARN-- [path002w] /usr/sbin/quota in root's PATH from default is not owned by root (owned by bin).
--WARN-- [path002w] /usr/sbin/quotacheck in root's PATH from default is not owned by root (owned by bin).
--WARN-- [path002w] /usr/sbin/quotao in root's PATH from default is not owned by root (owned by bin).
--WARN-- [path002w] /usr/sbin/quotas in root's PATH from default is not owned by root (owned by bin).
--WARN-- [path002w] /usr/sbin/repquota in root's PATH from default is not owned by root (owned by bin).
--WARN-- [path002w] /usr/sbin/warnquota in root's PATH from default is not owned by root (owned by bin).
```

```text
# Performing check of anonymous FTP...
--WARN-- [ftp003w] ~ftp/etc/passwd contains accounts with passwords.
```

```text
# Performing checks of mail aliases...
# Checking aliases from /etc/aliases.
```

```text
# Performing check of 'cron' entries...
-ERROR-- [init004e] '/systems/default/gen_cron' is not executable (command GEN_CRON_FILES).

# Performing check of 'services' and 'inetd'...
# Checking services from /etc/services.
-FAIL-- [inet003f] The port for service pop-2 is assigned to service pop2.
-ERROR-- [init006e] '/systems/default/inetd' does not exist (file INETDFILE).

# Performing NFS exports check...

# Performing check of system file permissions...
-WARN-- [permw] / should not have owner search.
-WARN-- [permw] / should not have group search.
-WARN-- [permw] /etc should not have owner search.
-WARN-- [permw] /etc should not have group search.
-WARN-- [permw] /bin should not have owner search.
-WARN-- [permw] /bin should not have group search.
-WARN-- [permw] /usr should not have owner search.
-WARN-- [permw] /usr should not have group search.
-WARN-- [permw] /usr/bin should not have owner search.
-WARN-- [permw] /usr/bin should not have group search.
-WARN-- [permw] /usr/lib should not have owner search.
-WARN-- [permw] /usr/lib should not have group search.
-WARN-- [permw] /var should not have owner search.
-WARN-- [permw] /var should not have group search.
-WARN-- [permw] /var/spool should not have owner search.
-WARN-- [permw] /var/spool should not have group search.
-WARN-- [permw] /dev should not have owner search.
-WARN-- [permw] /dev should not have group search.
-WARN-- [permw] /etc/aliases should not have owner read.
-WARN-- [permw] /etc/aliases should not have group read.
-WARN-- [permw] /etc/aliases should not have world read.
-WARN-- [permw] /etc/exports should not have owner read.
-WARN-- [permw] /etc/exports should not have group read.
-WARN-- [permw] /etc/exports should not have world read.
-WARN-- [permw] /etc/fstab should not have owner read.
-WARN-- [permw] /etc/fstab should not have group read.
-WARN-- [permw] /etc/fstab should not have world read.
-WARN-- [permw] /etc/group should not have owner read.
-WARN-- [permw] /etc/group should not have group read.
-WARN-- [permw] /etc/group should not have world read.
-WARN-- [permw] /etc/hosts.allow should not have owner read.
```
