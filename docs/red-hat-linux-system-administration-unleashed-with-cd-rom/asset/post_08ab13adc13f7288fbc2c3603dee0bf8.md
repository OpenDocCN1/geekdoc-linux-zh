
Rlogin has some support for interoperating with the X Window System, but it does not do quite as well as the more flexible Telnet protocol. Rlogin can communicate changes in window size from client to server, but it does not inform the server about the location of the user's X display.

## Authentication for the Trust-Based R-Commands

A proper understanding of the R-commands requires knowledge of how their trust-based authentication works. Take rlogind as an example. When it is launched by inetd and tcpd, rlogind starts by checking that the TCP port used on the client is in the range 512 to 1023 (inclusive). This check is done because on UNIX systems, only processes owned by root may use those ports. Next, it determines the IP address of the client, and looks up the hostname for that IP address. If the address and hostname do not match, the connection is dropped. It then reads the name of the client-side user from the connection, followed by the username that is desired on the server.

Next it attempts to authenticate the username supplied by the client for password-free access to the named account; the details of this authentication procedure and how to configure it are described in the next section, “Configuring Trust for the R-Commands.” Its final action is to launch login to actually allow the user to log in. If the authentication was successful, login is called with the -f argument; otherwise, login will prompt for a password as normal.

Clearly, the authentication scheme used by the R-commands relies on both the client machine and the communication medium being trustworthy. Note in particular that UNIX (and similar operating systems, including Linux) are unusual in restricting the use of low-numbered TCP ports; other operating systems, such as MacOS and Microsoft Windows, do not in general impose such restrictions. The R-commands are also particularly vulnerable to attacks that spoof hostnames or addresses, although running them from tcpd does help somewhat here. Also, even if users don’t rely on the R-commands’ willingness to permit logins without passwords, there is still the usual vulnerability of transmitting passwords in the clear.

Allowing systems to trust each other carries a definite risk; if one system is penetrated, any other system that trusts it is also vulnerable. Indeed, since there is no way to prove that other systems have not been compromised, an administrator must assume that they have been. This means that if a network uses R-commands, any security breach entails clean-up activity (such as re-installing the operating system) on all network hosts entering into a trust relationship.

Moreover, trust relationships are transitive. Suppose the host radish.example.com trusts cucumber.example.com but not pumpkin.example.com. The administrator of cucumber is less careful about trust relationships than the administrator of radish, so cucumber does trust pumpkin. Now, if pumpkin is penetrated, even though radish does not trust it directly, the attacker can also compromise radish, using cucumber as an intermediary. Obviously, large networks may have many trust relationships, which can make it harder to determine which hosts transitively trust others—especially if hosts are administrated by different people.

The R-commands were designed to operate in an environment where trust relationships between machines allow users to access network services without typing passwords. In the past, Internet usage was limited almost entirely to academic institutions, and in such contexts, it was often considered reasonable and helpful to trust users in this way. The wider use of the Internet in recent times has essentially eliminated environments of this sort, and it may well be the case now that the only situations in which it is sensible to rely on trust are those in which all the users are known, and the network is not connected to the wider Internet.

## Expressing Trust Relationships for the R-Commands

Once you have decided to allow two systems to trust each other, the next question is how to configure the R-commands to express this trust. As you have seen, the R-commands grant password-free access to trusted users on trusted hosts. The system assumes that accounts with the same name on different machines are owned by a single user. For this reason, trusted hosts are also called equivalent hosts: Users with some level of access on one host should have an equivalent level of access on another.

Red Hat Linux uses Pluggable Authentication Modules (PAM) for authentication, so the details of configuration differ slightly from traditional UNIX systems. However, the essentials are the same. The R-commands use a system-wide configuration file, /etc/hosts.equiv, as well as per-user files stored in $HOME/.rhosts. PAM configuration uses files in /etc/pam.d: for the R-commands, the relevant files are /etc/pam.d/rsh and /etc/pam.d/rlogin. These files contain lines such as

```
auth sufficient /lib/security/pam_rhosts_auth.so
```

You can add options to the end of this line to alter the way the authentication works.

## Granting Trust to Hosts and Users

The /etc/hosts.equiv file defines the hosts and users that are granted trusted (password-free) access to the R-commands on your system. Entries in this file contain a hostname, optionally preceded (with no intervening whitespace) by a plus sign. Naming a host grants it trusted status: Any user on that host is allowed to access a like-named account on the server. The hostname may optionally be followed by one or more trusted usernames, separated by whitespace, each of which is optionally preceded by a plus sign. Trusted users on a host are allowed password-free access to all accounts on the server except the root account.

Hostnames and usernames in /etc/hosts.equiv may be preceded by a minus sign instead of a plus sign, to explicitly deny trusted status. If a host is untrusted in this way, users on that host must supply a password to gain access; similarly, if a user is untrusted, that user on that host must supply a password. (See the section “Creating an .rhosts File” for more details on this.)

An entry can also consist of just a single plus sign. This allows access from any host in the world. This is clearly a significant security hole, so the PAM implementation disables this functionality by default. You can enable it by adding the option “promiscuous” to the pam_rhosts_auth module lines in /etc/pam.d/rsh and /etc/pam.d/rlogin.

Some examples will clarify the situation.

- pumpkin—Grants trusted access for any user on pumpkin to accounts of the same name.
- -pumpkin—Denies trusted access for any user on pumpkin to accounts on the server.
- pumpkin arc—Denies trusted access to the user on pumpkin named arc.
- pumpkin arc—Grants trusted access to all non-root accounts on the server for a user on pumpkin named arc.
- + arc—Grants trusted access to all non-root accounts on the server for a user on any host in the world named arc.

## Per-User .rhosts Files

Users may create an .rhosts file in their home directories. As a security measure, this file is ignored unless it is writable only by its owner, and is owned by either root or the user whose home directory it is in. Setting the privategroup option for the pam_rhosts_auth module additionally allows it to be group-writable as long as the group-owner has the same name as the user, and the user is the only member of that group.

Entries in the .rhosts file use the same format as those in /etc/hosts.equiv. They behave in almost exactly the same way, except that they grant or deny access only to that user’s account. Consider the following entry:

```
pumpkin arc
```

If this entry is in the /etc/hosts.equiv file, it grants the user arc trusted access to all accounts on the server. But if it is in the .rhosts for a user named bob, it allows trusted access only to bob’s account.
