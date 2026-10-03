really using when you connect to a host?

Use the -G option to ssh. It tells ssh(1) to parse all the configurations for the target host, print out the configuration it’s going to use, and immediately exit without connecting. You can review your settings to verify you’re getting what you need.

# SSH Jump Hosts

Sysadmins often have to pass through one host to get to another. Maybe you trust this intermediate host. Maybe you don’t. OpenSSH supports jump hosts, letting you use an SSH server as a relay to connect to a second server. Yes, you could do this manually by logging into the intermediate host and running ssh again, but using the built-in support means that the jump host sees none of your plain text. The jump host has no control over the options your client and the target server negotiate. This means you can, say, forward X or your SSH agent through a jump host that accepts neither.

Specify a jump host with -J. Add the username if needed.

```
$ ssh -J mw1@envy jerkface@pride
```

I’m trying to log in as jerkface on the host pride, using the account mw1 on host envy as a jump host. I’ll get prompted for my authentication credentials on the jump host, and then my credentials on the destination. It’s best to use public key authentication on both hosts.

Set a jump host in ssh_config with the ProxyJump keyword.

```
Host pride.mw1.io
ProxyJump mw1@envy.mw1.io
```

How much do you have to trust your jump host? None of your keystrokes reach the jump host, so you don’t have to worry about session logging. The only thing the jump host can see is an encrypted data stream between your client and the destination server. The jump host could alter or interrupt the encrypted stream, but that’s exactly the sort of tampering SSH is designed to detect.

Some Linux distributions disable jump hosts in their client.

# Addressing Options

The OpenSSH client lets you choose how it uses TCP/IP, by setting the address family and the source address.

# IP Protocol Version

Hosts can have both IPv4 and IPv6 addresses. The AddressFamily keyword tells the client to connect with only IPv4 (inet) or with only IPv6 (inet6). The default is any, which means “connect over whichever protocol the system resolver returns an address for.” Sometimes, you’ll have better connectivity over one protocol or the other. If you get your IPv6 connectivity via a tunnel, using only IPv4 for SSH might make sense. Similarly, if you have unlimited IPv6