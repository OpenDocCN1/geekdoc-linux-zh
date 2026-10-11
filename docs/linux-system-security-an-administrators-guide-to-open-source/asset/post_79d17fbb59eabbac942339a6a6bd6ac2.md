
# H

**Haval** A one-way cryptographic hash function. It produces a variable-length hash.

**HTTP** HyperText Transfer Protocol. The protocol used to transfer most of the HTML documents around the web.

# I

**IDEA** A block cipher algorithm operating on 64-bit data blocks using a 128-bit key. Originally used by PGP.

**inetd** A daemon that manages connections for a list of daemons found in `inetd.conf`. `inetd` listens for connection requests and will spawn the daemon.

**Internet Protocol Security (IPsec)** A protocol designed to provide authentication and confidentiality (encryption) for IPv6. While it is required to be supported, it is not required to be used. There is some support for IPv4.

# L

**LILO** Linux loader. Used to boot the Linux kernel or another operating system.

**logrotate** Highly flexible set of C programs to manage log files.

# M

**MD5** RSA Data Security, Inc., MD5 message digest algorithm. A cryptographic hash algorithm that produces a 128-bit hash of a message.

# N

**Naval Research Laboratory (NRL)** The Navy's corporate laboratory.

**Network File System (NFS)** A protocol that provides the ability to share data from one computer to another, transparently.

**Network Information Service (NIS)** A system that allows central management of services that may be shared by multiple machines, such as host-name information.

**one-time password (OTP)** A password system in which a supply of passwords are provided to be used only one time each. This prevents unauthorized access should the password be compromised.

**One-time passwords in everything (OTPE)** A set of replacement programs for UNIX to support one-time passwords.

**Open Group** A group dedicated to promoting integration of technology within and between enterprises. Formed in a merger with OSF and X/Open.

**Open Software Foundation (OSF)** Formed in 1988 to promote the development of open (free) software. Now a division of the Open Group.

**partition** A subsection of a disk.

**password database library (pwd library)** A library of routines that allow configurable access to and management of /etc/passwd, /etc/shadow, and network authentication systems including NIS and RADIUS.

**path** An environment variable used by shells and other programs containing a list of directories to be searched in order when an unqualified command is referenced.

**Perl** A powerful, free programming language.

**PGP signature** A cryptographic hash of a file, created with PGP.

**pluggable authentication modules (PAM)** Authentication modules provide a number of different ways in which a user may be authenticated.

**Point-to-Point Protocol (PPP)** Allows you to send protocols such as IP or IPX over a serial connection. Supports authentication and many options.

**portmapper** Daemon that provides mapping between the port on which an RPC program is listening and the program number used by that RPC program. A process attempting to communicate with an RPC program contacts the portmapper to get this information.

**Pretty Good Privacy (PGP)** A collection of utilities to generate signatures of files, provide encryption, and perform key management. Originally designed by Philip Zimmermann.

**process identifier (PID)** A number associated with a process running on the system. Assigned by the kernel and will be reused when the process terminates.

# R

**RADIUS** Remote authentication dial-in user service. Provides authentication and accounting information. Typically used with PPP servers but is also being applied to other services. Described in RFC 2138 and RFC 2139. There are several free implementations available.

**RAM** Random access memory. Fast memory that holds parts of the operating system and data currently being used.

**RFC** Request for comments. A proposal for an Internet standard or an informational document, written by a committee and subject to review. After a period of review, a proposal may become an Internet Standard.

**risk analysis** The process of analyzing a system for weaknesses in data integrity, availability, and confidentiality.

**rlogin** A command that allows users to gain remote access to a UNIX system. Considered to be an insecure protocol.

**RSA** Public key cryptosystem developed by Rivest, Shamir, and Adleman. The RSA algorithm keys use numbers that are computationally difficult to factor.

**rsh** Remote shell. A program that allows execution of a command on a remote UNIX machine. Many people do not allow the r-commands to be used on their systems because of problems with the security model.

# S

**SAMBA** A program that provides Microsoft file sharing service (SMB) on a UNIX machine. It provides both client and server support.

**Secure Shell (SSH)** A secure replacement for the r-commands.

**secure socket layer (SSL)** A collection of protocols that implement encryption tunnels at the Transport layer.

**server message block (SMB)** Also session message block. The Microsoft protocol used for file sharing.

**SGID** Set group identifier. A SGID program runs with effective group permissions of the group to which the file belongs.

**SHA-1** A cryptographic hash algorithm designed by NIST and NSA. Produces a 160-bit hash.

**shadow file** A non-world-readable file that contains encrypted passwords and information about password expiration.

**signature file** A file containing the cryptographic hash of another file. Used to verify the authenticity and integrity of the original file. In the case of `tiger`, signature files contain multiple signatures along with the name of the file with which the signature is associated.

**Snefru** A one-way cryptographic hash function. Messages are hashed into 128- or 256-bit values.

**standard password format (SPF)** A format used by many UNIX operating systems, wherein each field in order contains the value of a prescribed piece of information.

**SUID (Set User Identifier)** An SUID program runs with the effective permissions of the owner of the file.

**superuser do (sudo)** A program that provides configurable, controlled root privileges and an audit trail of which commands were executed by whom.

**syslog** A daemon that accepts messages from other processes and logs them to a file or the console window if the level and facility of the message match or exceed those specified in the syslog configuration file.

# T

**TCP** Transmission Control Protocol. A connection-oriented networking protocol.

**TCP_wrappers** A set of programs that provide extensive logging and authorization control over programs compiled with `libwrap` or those started from `inetd`.

**telnet** A program that allows users to log in from one computer to a remote computer.

**Transparent Cryptographic File System (TCFS)** Similar to CFS, but implemented as a kernel module.

**Tripwire** A utility to record fingerprints of UNIX files and to notify you if anything changes.

# U

**UDP** User Datagram Protocol. A connectionless networking protocol.

**UNIX** A popular operating system developed by Ken Thompson and Dennis Ritchie.

**user identification number (UID)** A number representing a particular user name. Used by the kernel and other programs. `/etc/passwd` provides mapping between the number and the name.

# X

**xinetd** A more secure replacement for inetd.

# INDEX

## Symbols

- `$HOME/.netrc`, 36
- `$HOME/.rhosts`, 36
- `/bin/ksh`, 65
- `/etc/fstab` See filesystem
- `/etc/gpasswd`, 69
- `/etc/hosts.allow`
  - and portmap, 223
  - and SSH, 266, 270, 283, 310
  - and TCP_wrappers, 202–216
- `/etc/hosts.deny`
  - and portmap, 223
  - and SSH, 266, 270, 283, 303, 310
  - and TCP_wrappers, 202–216
- `/etc/hosts.equiv`, 36
- `/etc/inetd.conf`, 33, 34, 521
- `/etc/inittab`, 24
- `/etc/issue`, 94
- `/etc/issue.net`, 94
- `/etc/lilo.conf`, 22, 423
- `/etc/login.defs`, 61, 63–64
- `/etc/logrotate.conf`, 156, 495
- `/etc/logrotate.d`, 156, 495
- `/etc/nologin`, 94, 144
- `/etc/oelaccess` See OPIE
- `/etc/opiekeys` See OPIE
- `/etc/pam.d` files See PAM
- `/etc/passwd` See password
- `/etc/pwdb.conf`, 87
- `/etc/rc.d/init.d/syslog`, 170
- `/etc/rc.d/rc.local`, 94
- `/etc/security`, 68, 93, 190
- `/etc/security` files See PAM
- `/etc/services`, 33
- `/etc/shadow` See shadow file
- `/etc/skeykeys` See S/Key
- `/etc/sudoers` See sudo
- `/etc/syslog.conf`, 160–166
- `/etc/xinetd.conf` See xinetd, 232
- `/lib/security` See PAM
- `/sbin/init`, 24
- `/sbin/lilo`, 23, 424
- `/var/run/utemp`, 25
- `/var/log/passwd` See system accounting
- `/var/log/xferlog`, 159, 166

## A

- ac See system accounting
- acceptable use policy (AUP), 15, 547
- accton See system accounting
- AFCERT, 529
- AntiSmurf, 38
- Artistic License
  - and Crack, 314
- attacks, 4–7
  - hijacking, 5
  - TCP/IP, 5
  - See also exploits
- auditd, 171
- AusCERT, 529
- authentication, 42
  - See also PAM
- Autonomous Agents for Intrusion Detection (AAFD), 543

## B

- back doors, 4
- backups, 49, 523, 525
- BIOS, 22
- break-in recovery, 526
- buffer overflow, 5
- bugtraq, 535, 538–539, 547

## C

- Caldera, 530
- CERT, 530, 539
