The **ssh** command can also be used to execute a command on the remote computer. For example, if you wanted to monitor the messages file on a remote computer for a minute, you could type the following command:

```
```
# ssh root@maple "tail -f /var/log/messages"
root@maple's password:
```
```

After you typed the password in the preceding case, the last several lines of the /var/log/messages file on the remote computer would be displayed. As messages were received, they would continue to be displayed until you decided to exit (press Ctrl+C to exit the tail command).

> **NOTE:** To learn how to use public keys for passwordless login to ssh, refer to Chapter 14. Find out more about the ssh command from the SSH Web site (http://www.openssh.org).

# Using scp for remote file copy

The **scp** command is a simple yet secure way of copying files among Linux systems. It uses the underlying ssh facility, so if ssh is enabled, so is scp. Here is an example of using scp to copy a file from one computer to another:

```
```
# scp myfile toys.linuxtoys.net:/home/chris
root@toys.linixtoys.net's password: ******
```
```

In this example, the file myfile is copied to the computer named toys.linixtoys.net in the /home/chris directory. If you don’t provide a user name, scp assumes you are using the current user name. Unlike some tools that provide remote login, scp and ssh do allow you to log in as root user over the network, by default. (Many people turn off this feature for security reasons.)

To use scp with a different user name, you can append the user name with an @ character. For example, chris@toys.linixtoys.net:/home/chris would attempt to log in as the user named chris to do the file copy.

The first time you connect to a remote computer using scp or ssh, those commands try to establish the authenticity of the remote host. If it cannot establish the host’s authenticity, it will display the RSA key fingerprint and ask you if you want to continue. If you type yes, scp will not question the authenticity of that computer again for subsequent scp commands.

However, if the RSA key fingerprint should change in the future for the remote computer (which will happen if, for example, the operating system is reinstalled on that computer), scp will refuse to let you connect to that remote computer. To override that refusal, you need to edit your $HOME/.ssh/known_hosts file and delete the entry for the remote computer. You can then verify the authenticity of the remote computer and continue to use scp.

The sftp command, which also communicates using secure ssh protocols, is a command for copying files from an FTP server. It is considered a more secure way of getting files from an