alphanumeric characters representing the public key, and a comment field. Each entry goes on a single line, no matter how long it is. It will look something like this:

```
ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAA... wE2Ime8Rs/Q== moose-20160525
```

This is an RSA key, as shown by ssh-rsa at the beginning of the entry. This public key begins with a AAA and ends with 8Rs/Q==. Many but not all public-key entries end in the double equals sign. The comment at the end gives the host this key was created on and the date of creation.

You can put additional keywords and instructions on how this key may be used at the beginning of the entry. The server obeys those instructions, within the limits of the user’s permissions. Find a complete list of authorized_keys keywords in the sshd(5) man page, but here are the most commonly used ones.

# command="command"

Whenever someone logs in using this key, run the specified command. SSH ignores any command provided by the user in favor of the one dictated by authorized_keys. You might use this for automated processes, such as configuring a VPN (Chapter 13) or running rsync.

```
command="sudo ifconfig tun0 inet 192.0.2.2/30" ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAA...
```

One interesting feature is that SSH retains any command the client requested in the environment variable $SSH_ORIGINAL_COMMAND. You can have authorized_keys run a script that checks this environment variable and acts appropriately. (“The backup account just requested access to /bin/bash? Hello, sysadmin, we have a problem…”)

# environment="NAME=value"

This set an environment variable when this key is used to log in. You can use any number of environment statements.

```
environment="automated=1" ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAA...
```

By default, sshd does not permit setting environment variables. The sysadmin must set PermitUserEnvironment to yes in sshd_config for users to set environment variables.

# from="ssh-pattern"

This key can only be used for authentication if the clients address or reverse DNS matches the given pattern. We discussed patterns in Chapter 2. I frequently use this to restrict automated processes. Even if an intruder steals a private user key, he cannot access the SSH server from any host other than the one I permit.

```
from="198.51.100.0/29" ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAA...
```

Only hosts in the IP range 198.51.100.0 through 198.51.100.7 can use this key to log into the SSH server.

You can only use host names in the pattern if UseDNS is set to yes.

Remember that intruders can frequently forge their reverse DNS entries, so it’s