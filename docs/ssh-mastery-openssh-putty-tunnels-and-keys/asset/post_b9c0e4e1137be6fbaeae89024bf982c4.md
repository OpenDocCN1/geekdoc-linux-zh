
While OpenSSH offers options to easily change the algorithms supported and its preference for each, don’t! Programmers with more cryptography experience than both of us together arrived at OpenSSH’s encryption preferences after much hard thought, troubleshooting, and suffering. Gossip, rumor, and innuendo might crown Blowfish as the awesome encryption algorithm du jour, but that doesn’t mean you should tweak your OpenSSH server to use that algorithm and no other.

The most common reason people offer for changing the encryption algorithms is to improve speed. SSH’s primary purpose is security, not speed. Do not abandon security to improve speed. You might encounter a device that only speaks older encryption algorithms. We’ll cope with those in Chapter 15, “OpenSSH Scraps.”

Now that you understand how SSH encryption works, leave the encryption settings alone.

## Chapter 2: Common Configuration

The OpenSSH client and server share a common configuration syntax. We’ll discuss these common elements before delving into the details of either application. Sysadmins familiar with Unix-like systems should have no trouble with OpenSSH configuration.

All system-wide OpenSSH configuration files reside in `/etc/ssh` by default. Some operating systems use an alternate location—for example, OSX uses `/private/etc/ssh` but symlinks `/etc/ssh` there, while FreeBSD’s add-on `openssh-portable` package uses `/usr/local/etc/ssh`. Once you find the configuration directory, you’ll find a pretty standard set of files.

Default settings for the `ssh(1)` client appear in `ssh_config`.

The files starting with `ssh_host` and ending in `_key` are the server’s private keys. The middle of each file name gives the encryption algorithm—for example, `ssh_host_ecdsa_key` contains the host key that uses the ECDSA algorithm. These files should only be readable by root.

Each private key has a corresponding file with the same name but an added `.pub` at the end. This is the public key for that file. The server will offer the content of these files to any client.

Finally, `sshd_config` contains the server configuration. While you can tweak `sshd` with command-line options, permanent configuration is handled in the configuration file.

Both configuration files consist of a series of keywords, followed by the value that keyword is set to. These values can have any format that makes sense for the configuration target. Here’s how OpenSSH sets one common value.

```
Port 22
```

The keyword Port is set to 22. Presumably this makes sense for whatever the Port keyword is intended to represent. We’ll get to what that is in Chapter 3, “The OpenSSH Server.” You’ll also see keywords set to file paths. Here we see the value HostKey set to a file path in the `/etc/ssh` directory.

```
HostKey /etc/ssh/ssh_host_ed25519_key
```

Follow existing examples when setting any keyword. Always refer back to the man pages if you have trouble.

The pound sign (`#`) indicates a comment. Everything on a line after a comment is ignored. The OpenSSH crew distributes their configuration files with all options set to the default and commented out. While `sshd(8)` requires a configuration file to start, you can create a valid, useful, and working configuration with `touch sshd_config`. The SSH client and server run just fine with everything at the default setting. The commented-out settings are provided as a convenient reference, that’s all.

To change the defaults, remove the pound sign and change the value.

### Multiple Values

Some environments need keywords set to multiple values. How you set those values depends on the keyword. Keywords like HostKey and Port can appear multiple times, each with a separate value.

```
Port 22
```

```
Port 2222
```

Keywords like Host accept multiple values, separated by a space.

```
Host envy.mwl1.io avarice.mwl1.io
```

Other keywords, such as Address, expect comma-separated values.

```
Address 192.0.2.0/25, 198.51.100.0/24
```

If ssh(1) or sshd(8) complains about a configuration, verify that you’re separating multiple entries correctly. This book contains many examples of assigning multiple values, but the OpenSSH manual is always the final word.

### Wildcards in OpenSSH Configuration Files

Configuration files for the OpenSSH server and client accept wildcards, called patterns. Rather than listing all possible values of a configuration setting, patterns let you say “anything that matches this expression.” Wildcards are most often used for Match rules, as discussed in “Conditional Configuration with Match” later this chapter. Patterns let you write configuration statements such as “all hosts in this domain” or “all IP addresses in this network.” The two wildcard characters are:

- ? matches exactly one character
- * matches zero or more characters

For example, I could use a pattern to set the value of the Host keyword to any host in mwl.io.

```
Host *.mwl1.io
```

If I used the question mark wildcard, this pattern would match any host with a one-character hostname. Very few environments segregate security domains by the length of the hostname, but if they did, you could use multiple question marks to identify them. This pattern matches sloth.mwl1.io and wrath.mwl1.io, but not gluttony.mwl1.io or avarice.mwl1.io.

```
Host ??????.mwl1.io
```

Patterns are also useful for IP addresses. Here I match the hosts 203.0.113.10 through 203.0.113.19.

```
Address 203.0.113.?
```

If I use the asterisk wildcard, I can match any IP within a /24 network.

```
Address 203.0.113.*
```

You might use netmasks with IP address ranges, as discussed in Chapter 5. Negate patterns by putting an exclamation point in front. This pattern matches everything except hosts in mwl.io.

```
Host !*.mwl.io
```

Negation is most useful when combined with a larger entity—that is, to say “Match everything except that one little piece.” If I want to match every host in mwl.io except for the customers in the subdomain vermin.mwl.io, I could use this pattern. Not all keywords support negation; you’ll have to try it and see if it works in your environment.

```
Host !vermin.mwl.io *.mwl.io
```

The lead OpenSSH developer describes negation as “a little fiddly.” I call it “likely to pull a shiv on you.” If you need negation, test thoroughly.

### Conditional Configuration with Match

Your server might need to behave differently depending on the source address or hostname of an incoming connection, or the username. An SSH client might need to use a different username for a particular group of hosts, or to activate X forwarding (Chapter 9) when used on the local network. The Match sshd_config keyword lets you establish special configurations for such situations.

Follow each Match statement by a set of conditions that trigger the match, then by a series of configuration statements OpenSSH should apply to connections that meet all of those conditions. We’ll see several examples in the next sections.

Before implementing a Match statement, configure OpenSSH for the most common setting. For example, if you are configuring sshd, you might want to deny X forwarding to all but select users. Configure sshd to deny X forwarding, then use a Match statement to check the username and permit X forwarding to matching users. While we haven’t covered X forwarding yet, denying it is a single entry in sshd_config.

```
X11Forwarding no
```

In all of the examples below, such an entry appears near the beginning of sshd_config as a default setting that we’ll selectively override.

You cannot use Match statements to adjust all possible ssh_config and sshd_config keywords. Check the manual pages for the complete list of supported keywords.

### Matching Users and Groups

The most common situation I encounter is when I want to enable an option for a particular user or group. The User or Group Match terms permit this.

```
X11Forwarding no
Match User mwlucas
X11Forwarding yes
```

I am always permitted to use X forwarding, as my awesome psychic powers eliminate all possible security risks.

If all of my system administrators share these powers, or if I settle for
