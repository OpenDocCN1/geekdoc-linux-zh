more -d’s until you are no longer curious.

# Configuring sshd(8)

This chapter discusses some generally useful sshd(8) options. Most sshd_config options appear in the chapter where they’re most useful—that is, options affecting X forwarding appear in Chapter 8, “X Forwarding,” while certificate options appear in Chapter 14, “Certificate Authorities.”

The version of OpenSSH shipped with your operating system might not support all of the keywords described in this book. I’ve written this based on OpenSSH 7.6. Some operating systems either ship older versions, or deliberately remove functions for their own reasons. If a configuration option doesn’t work on your server, consult your operating system documentation or ask your vendor.²

# Set Host Keys

The HostKey keyword gives the full path to a file containing a private key. Each supported encryption algorithm uses a separate file.

```
HostKey /usr/local/etc/ssh/ssh_host_rsa_key
HostKey /usr/local/etc/ssh/ssh_host_ecdsa_key
HostKey /usr/local/etc/ssh/ssh_host_ed25519_key
```

The default files are named after the type of key they contain. The file ssh_host_rsa_key contains an RSA key, ssh_host_ed25519_key is an ED25519 key, and so on. This isn’t mandatory—OpenSSH will figure out what type of key is in a file and load it if appropriate—but it’s definitely the best practice. Putting your RSA key in a file named after ED25519 will confuse everyone.

Different operating systems handle missing key files differently. BSD-style and Red Hat-based systems automatically create missing key files. Many Linux systems require the sysadmin to manually create missing key files, but integrate key creation into their usual system administration tools. For example, Debian-based systems create missing key files when you run dpkg-reconfigure openssh-server.

Chapter 7, “SSH Keys,” covers creating host keys using OpenSSH’s native tools.

# Network Options

You can control how sshd(8) uses the network, from the version of IP all the way to the TCP port.

```
Port 22
AddressFamily any
ListenAddress 0.0.0.0
ListenAddress ::
```

The Port keyword controls the TCP port sshd uses. Internet standards call for SSH to run on port 22. Some organizations use a different port for SSH in the hope of improving security. Running SSH on an unusual port won’t actually