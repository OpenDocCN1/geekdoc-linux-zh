changed that keyword. The PubkeyAuthentication keyword must be set to yes.

```
PubkeyAuthentication yes
```

Now restart sshd, either with the built-in system command or pkill -1 sshd.

Changing sshd_config will not change how other programs use passwords. If you use passwords for sudo, sudo will still ask users for their password.

# Password Authentication Warning!

If you make a mistake in configuring SSH such that nobody can login, you can lock yourself out of your server. When making changes to sshd_config, do not log out of your existing SSH session until you verify your changes work.

(Remember, you can run sshd on an alternate port for testing, as discussed in Chapter 3.) Create a new SSH session. Verify that you can login and become root before disconnecting your first session.

The preceding paragraph is very important. Ignore it at your peril, or be prepared for your own manic-depressive gelato binge.

# Permitting Passwords from Specific Hosts

While passwords are weak, sometimes you cannot disable them entirely. You might have a few users or applications that cannot use keys for one daft reason or another. The underlying problems are most often political rather than technical, but they’re still problems. While you’re working on solving those problems, you can allow passwords from specific hosts with conditional configuration, as discussed in Chapter 3. Here, we allow password authentication from a particular subnet.

```
Match Address 192.0.2.0/24
PasswordAuthentication yes
```

Remember, all Match statements go at the bottom of sshd_config.

It is possible but extremely unwise to permit password authentication based on username. The SSH server, rather than hanging up on clients that request passwords, must get the username before hanging up on the client. This means that the Hail Mary Cloud will continuously poke at the server. The reasons that compel you to permit limited password authentication probably make requiring a strong password just as problematic—the same boss that demands he be allowed to use passwords probably thinks that p455w0rd is a secure password. The account that permits passwords will be a weak spot. The only thing that can save you here is good off-host logging to a very secure bastion host, so that when the machine is compromised you can tell the boss that the downtime is his fault.

# Agent Forwarding

Suppose I disabled password-based authentication on all my computers. The only way to access a command prompt on any of my hosts is by authentication with public keys. I’m working on my server wrath, and must copy a file over to