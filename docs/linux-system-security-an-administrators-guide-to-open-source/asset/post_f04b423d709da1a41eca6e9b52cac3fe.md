
147

## WHICH OTP SYSTEM SHOULD I USE?

There are advantages and disadvantages to both S/Key and OPIE. We will outline some of them here.

## Advantages and Disadvantages of S/Key

- Incorporates keysh and su allowing for ubiquitous implementation of OTP
- Offers OTP replacements for login and ftp
- Requires Linux password before OTP list may be (re)initiated by users other than root.
- PAM module dated
- Uses MD4 hash algorithm which is considered to be less secure than MD5
- Only warns the user if a secret key is about to be sent over the network

## Advantages and Disadvantages of OPIE

- Uses MD5 or MD4
- Offers OTP replacements for su, login, and ftp
- By default, disallows any user from passing the secret passphrase over the network
- Has a working PAM module
- Has no equivalent to keysh
- Does not require authentication to (re)initiate OTP list

## S/Key and OPIE VULNERABILITIES

The major vulnerability with S/Key and OPIE is the choice of secret key, password, or passphrase (we will refer to as passphrases here), respectively. Choosing good passphrases will make it more difficult for a bad-guy to guess them. Also, choosing passphrases that are not simple sentences will prevent them from being easily guessed by utilities such as Crack (discussed in Chapter 12), which could be configured to guess passphrases for S/Key or OPIE.

As added protection, consider further protecting /etc/opiekeys and/or /etc/skeykeys by setting their permissions to read/write by root only. This will disallow users other than root from using opieinfo and keyinfo, but it will also make it more difficult for bad-guys to glean information that could be used in guessing attacks.

If you need to implement access control, avoid using `/etc/optieaccess` or `/etc/skey/access` and instead use other access control mechanisms such as `TCP_wrappers` and various PAM modules like `pam_listfile`.

## SUMMARY

In this chapter, we looked at two publicly available one-time password programs, S/Key and OPIE. Each of these programs can substantially reduce the risks associated with system access by utilizing a password only once. This eliminates the capturing of static passwords via a network sniffer.

### For Further Reading

#### Programming

1. Loukides, Mike, and Andy Oram, *Programming with GNU Software*, Sebastopol, California, O'Reilly & Associates, Inc., 1997.
2. Oram, Andrew, and Steve Talbott, *Managing Projects with make*, Sebastopol, California, O'Reilly & Associates, Inc., 1991.

#### E-Mail Lists

You may subscribe to the `skey-users` mailing list by sending an e-mail message with the keyword `subscribe` in the body of the message to

```
skey-users-request@research.telcordia.com
```

Subsequently, you may post messages to `skey-users@research.telcordia.com`. Both S/Key and OPIE are discussed on this list.

## CHAPTER 7

## Bean Counting

## System Accounting

Although originally not designed for security purposes, Linux system accounting can provide valuable information about various activities taking place on your system. After a brief overview, this chapter discusses the appropriate security elements of system accounting and some situations for using it.

## GENERAL SYSTEM ACCOUNTING

Originally system accounting was developed for the purpose of keeping track of user resource consumption so that charges could be made against that user's account. In the days of mainframes and minicomputers, this was, in part, the way that Management Information Systems (MIS) departments got their funding. With the advent of personal workstations, the use of system accounting for that purpose has declined.

The Linux implementation of system accounting does not include many of the postprocessing scripts and configuration files (such as chargefee and the /var/adm/fee found on Solaris, IRIX, and other commercial UNIX systems) for fiscal accounting purposes, but it does include much (if not all) of the data required for such computations. Instead, Linux focuses on providing connection and process accounting information, each of which is described in detail in this chapter.

This is not the only source of information relating to activity on a Linux system. We saw in *PAM Logs* on page 109 of Chapter 5 that a great deal of connection and user activity information is maintained by PAM through *syslog*. We will explore many other mechanisms that provide such information throughout this book. Here we discuss connection and process accounting as it relates to enhancing overall system security.

## CONNECTION ACCOUNTING

Connection accounting is the tracking of current user sessions and user logins and logouts. It is handled in Linux through the *wtmp* (for active user sessions) and *utmp* (for login/logout records) facilities. The *wtmp* utility also maintains rebooting and system state change (via *init*) information. Various programs participate in the updating and maintenance of these utilities, so there is no specific daemon or program that must be run; however, the files for *utmp* and *wtmp* output must exist. The absence of these files effectively turns off connection accounting. All data associated with *utmp* and *wtmp* are collected in the files */var/run/utmp* and */var/log/wtmp*, respectively. These files are owned by root and the permissions are set to 644 ( *rw-r-r--* ). The data in these files are not in human-readable form. There are various utilities to convert the raw *utmp* and *wtmp* data into legible formats, among these are those listed in Table 7.1. As mentioned in the table, *dump-utmp* converts raw connection accounting data into ASCII formatted data. It is parsable because it separates each field in a record with | character, and it separates each record (or line of data) with a newline (carriage return) character. If you need to process the available data in these files beyond the capabilities of the other commands listed in the table, this command may be of use.

| Command | Description |
| :--- | :--- |
| dump-utmp | Converts the raw data from */var/run/utmp* or */var/log/wtmp* into ASCII-parsable format. Good for use with custom scripts. |
| ac | Prints out the connect time in hours. By default it generates a summary for all users. Various flags cause this command to output connect times on a per-user basis or daily basis or a combination thereof. This command reads */var/log/wtmp*. |
| last | Shows a listing of last logged-in users, including login time, logout time (or still logged-in message), device associated with the connection, and hostname of the connection, if not local. Also records reboots and runlevel changes through *init*. It reads */var/log/wtmp*. |
| who | Shows a listing of currently logged-in users. It reads */var/run/utmp*. |

The **ac** command provides summary statistics regarding user connections. Example 7-1 shows truncated output from ac with the d and f flags. The d flag shows the daily total, and the f flag breaks up the total connection time in hours on a per-user basis. This type of statistical information may be useful in user profiling and other activities related to intrusion detection (see Intrusion Detection on page 172 in Chapter 8 for further references regarding intrusion detection). The **last** and who commands are the most likely commands that you will use on a regular, security-perceptive basis.

### Example 7-1 Connection Summary Using ac

```
# ac -dp
  mary              8.10
  joe              135.87
  root               72.00
  Feb 24 total    215.97
  joe               64.80
  jane              50.20
  root              24.00
  guest              0.40
  mary               34.48
  Feb 25 total    172.88
#
```

### The last Command

As noted in Table 7.1 on page 150, the **last** command provides per-user login times, logout times, and locations as well as system reboot and run-level change information. Example 7-2 shows the execution of last with the -10 option. The -10 option is used here simply to limit the output of last to the most recent 10 entries. By default last will list every connection and run-level change recorded in /var/log/wtmp. In Example 7-2, we see that Mary has logged in from a system called roadrunner numerous times. The final entry shows that she logged in on Wednesday, February 24, at 3:53 P.M. and remained connected for 1 day, 20 hours, and 22 minutes. The record with no hostname indicates a local login (tty1, in this case).

### Example 7-2 Output of last

```
# last -10
mary     tty3      roadrunner     Fri Feb 26 09:14 - 11:46 (02:32)
mary     tty2      roadrunner     Fri Feb 26 08:27 - 09:57 (01:30)
mary     tty3      roadrunner     Thu Feb 25 18:55 - 18:58 (00:02)
billy    tty4      underdog       Thu Feb 25 18:54 - 18:55 (00:00)
merry    tty1                 Thu Feb 25 18:27 - 18:33 (00:05)
     reboot                 Thu Feb 25 13:45 - 13:45 (00:00)
joe      tty3      roadrunner     Thu Feb 25 13:44 - 13:45 (00:01)
guest    tty3      roadrunner     Thu Feb 25 13:45 - 13:45 (00:00)
guest    tty3      roadrunner     Thu Feb 25 09:53 - 10:15 (00:22)
mary     tty1      roadrunner     Wed Feb 24 15:53 - 12:16 (1+20:22)
```

The value of the **last** command from a security viewpoint is that it provides a way to quickly review connection activity on a given system. Glancing through the output on a daily basis is a good habit to get into and will allow
