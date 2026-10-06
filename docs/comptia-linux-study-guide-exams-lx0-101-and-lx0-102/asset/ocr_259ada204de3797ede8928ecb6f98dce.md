5. Add the contents of the file you've just transferred to the end of ~/.ssh
/authorized_keys.file. (This file is sometimes called ~/.ssh/authorized_keys, so
you should check to see which is present. If neither is present, you may need to
experiment) Typing `cat ~/temp.rsa >> ~/.ssh/authorized_keys` should do this job,
if you stored the original file as ~/temp.rsa.

6. On some systems, you may need to modify permissions on the ~/.ssh/authorized_\keys file and on the directories leading to it. The authorized_keys file may require
0600 permissions, and you may need to remove write permissions for any but the
account's owner on your home directory and not ~/.ssh directory.

If you now log out of the SSH server system and try to log in again SSH from the authen-
tication automatically. If this doesn't work, chances are the ~/.ssh/authorized_keys file
need another name, as described earlier. You may also want to check that the file includes
a line matching the contents of the original public-key file on the client. Some older clients
may require you to specify that you use version 2 of the SSH protocol by using the -2
option:

```
$ ssh -2 server
```

# Using ssh-agent

Another SSH authentication option is to use the ssh-agent program. This program
requires a password to initiate connections, so it's more secure than configuring logins
without passwords; however, ssh-agent remembers your password, so you need type it
once per local session. To use ssh-agent, follow these steps:

+   1. Follow the procedure for enabling no-password logins described in "Configuring
Logins Without Passwords," but with one change: Omit the -N option from the\ssh-keygen command in step 2. You will be asked for a passphrase at this step. The
phrase will be your key for all SSH logins managed by ssh-agent.
2. On the Client system, type ssh-agent /bin/bash. This launches ssh-agent, which
in turn launches bash. You will use this bash for subsequent SSH logins.
3. In your new system, type ssh-add ~/.ssh/id_rsa. This adds your RSA key to the
managed by ssh-agent. You will be asked to type your SSH passphrase at this
time.

From this point, whenever you use SSH to connect to a remote system to which
yve given your public key, you won't need to type a password. You will, however,
repeat steps 2 and 3 when you log out, and the benefits will accrue only to the shell
ing step 2 or any shells you launch from that.

If you have used this facility, you can insert ssh-agent into your normal login
procedure. For instance, you can edit /etc/passwd so that the ssh-agent /bin/bash is your
login shell. For a GUI login, you can rename your normal GUI login script (for instance,
change ~/.session to ~/.session-nossh) and create a new GUI login script that calls\ssh-agent with the renamed script as its parameter. Either action inserts ssh-agent at the
root of your user process tree so that any call to SSH uses ssh-agent.