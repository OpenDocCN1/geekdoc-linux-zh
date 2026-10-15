```
Welcome to Caitlin
Running Ubuntu

* All access is logged *

login: paul
Password:
Last login: Sat Jul 9 12:05:41 from 10.0.0.5
[paul@caitlin ~]$
```

# TIP

Note that the server responds with Welcome to Caitlin, running Ubuntu, which is a customized message. Your machine will probably respond with Ubuntu and some version information. This is insecure: giving away version numbers is never a smart move. In fact, even saying Ubuntu is questionable. Edit the issue and issue.net files in your /etc directory to change these messages.

Running the w command now shows you as connecting from the external IP address.

# Telnet Versus SSH

Although Telnet is worth keeping around as a fail-safe, last resort option, SSH is superior in virtually every way. Telnet is fast but also insecure. It sends all your text, including your password, in plain text that can be read by anyone with the right tools. SSH, on the other hand, encrypts all your communication and so is more resource-intensive but secure—even a government security agency sniffing your packets for some reason would still have a hard time cracking the encryption.

> Andy Green, posting to the fedora-list mailing list, summed up the Telnet situation perfectly when he said, “As Telnet is universally acknowledged to encourage evil, the service telnetd is not enabled by default.” It is worthwhile taking the hint: Use Telnet as a last resort only.

# Setting Up an SSH Server

If not installed already, the OpenSSH server can be installed through Synaptic by adding the openssh-server package. If you have disabled it, you can re-enable it by selecting System, Administration, Services and selecting the Remote Shell Server box. As you might have gathered, sshd is the name for the SSH server daemon.

Two different versions of SSH exist, called SSH1 and SSH2. The latter is newer, is more secure, comes with more features, and is the default in Ubuntu. Support for SSH1 clients is best left disabled so older clients can connect. This is set up in the /etc/ssh/sshd_config file on this line:

```
#Protocol 2,1
```