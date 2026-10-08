# Advanced Bash-Scripting Guide

```
# Pass a different 'USERNAME' 'HOSTNAME' if desired:
USER=$(USERNAME)-$(whoami)
HOST=$(HOSTNAME)-$(hostname)

# Execute the above command-line on the remote host,
## with all transmissions encrypted.

ssh -l ${USER} ${HOST} "ls -l"

# The expected result is a listing of your username's home
## directory on the remote machine.
# To see any difference, run this script from somewhere
## other than your home directory.

# In other words, the Bash command is passed as a quoted line
# to the remote shell, which executes it on the remote machine.
# In this case, ssh does `bash -c "ls -l*"` on your behalf.

# For information on topics such as not having to enter a
## password/passphrase for every command-line, see
## man ssh
## man ssh-keygen
## man sshd_config.
```

Within a loop, ssh may cause unexpected behavior. According to a Usenet post in the complex/unix shell ssh inherits the loop's stdin. To remedy this, pass ssh either by the -n or -f option.

Thanks, Jason Bechtel, for pointing this out.

scp Secure copy, similar in function to rcp, copies files between two different networked machines, but does so using authentication, and with a security level similar to ssh.

# Local Network

# write

This is a utility for terminal-to-communication. It allows sending lines from your terminal (console or xterm) to that of another user. The msg command may, of course, be disabled to write access to a terminal

Since write is interactive, it would normally not use in a script.

# netconfig

A command-line utility for configuring a network adapter (using DHCP). This command is native to Red Hat centric Linux distros.

# Mail

# mail

Send or read e-mail messages.

This stripped-down command-line mail client works fine as a command embedded in a script.

Chapter 16. External Filters, Programs and Commands 289