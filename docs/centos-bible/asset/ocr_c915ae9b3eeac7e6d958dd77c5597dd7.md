# Part II Using CentOS

After you typed the password in the preceding case, the last several lines of the /var/log/messages file on the remote computer would be displayed. As messages were received, they would continue to be displayed until you decided to exit (press `Ctrl`+`C` to exit the `tail` command).

> NOTE To learn how to use public keys for password-less login to `ssh`, refer to Chapter 13. Find out more about the `ssh` command from the SSH web site ([www.openssh.org](http://www.openssh.org)).

# Using `scp` for Remote File Copy

The `scp` command is a simple yet secure way of copying files among Linux systems. It uses the underlying `ssh` facility, so if `ssh` is enabled, so is `scp`. Here is an example of using `scp` to copy a file from one computer to another:

```
```
# scp myfile toys.linuxtoys.net:/home/chris
root@toys.linuxtoys.net’s password: ******
```
```

In this example, the file `myfile` is copied to the computer named `toys.linuxtoys.net` in the `/home/chris` directory. If you don't provide a username, `scp` assumes that you are using the current username. Unlike some tools that provide remote login, `scp` and `ssh` do allow you to log in as the `root` user over the network, by default. (Many people turn off this feature for security reasons.)

To use `scp` with a different username, you can append the username with an `@` character. For example, `chris@toys.linuxtoys.net:/home/chris` would attempt to log in as the user named `chris` to do the file copy.

The first time you connect to a remote computer using `scp` or `ssh`, those commands try to establish the authenticity of the remote host. If it cannot establish the host's authenticity, `scp` will display the RSA key fingerprint and ask you if you want to continue. If you type `yes`, `scp` will not question the authenticity of that computer again for subsequent `scp` commands.

However, if the RSA key fingerprint should change in the future for the remote computer (which will happen if, e.g., the operating system is reinstalled on that computer), `scp` will refuse to let you connect to that remote computer. To override that refusal, you need to edit your `$HOME/.ssh/known_hosts` file and delete the entry for the remote computer. You can then verify the authenticity of the remote computer and continue to use `scp`.

The `sftp` command, which also communicates using secure ssh protocols, is a command for copying files from an FTP server. It is considered a more secure way of getting files from an FTP server that has an `sshd` server running. The `sftp` command can be disabled by the server by commenting out the `sftp` line in the `sshd_config` directory.