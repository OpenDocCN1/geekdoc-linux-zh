reboot), you need to start all over. With `wget`, you can choose to restart a download and have it continue right where it left off. This has been a lifesaver for me on many occasions.
Let's say that you were downloading a 4GB DVD ISO image named `mydvd.iso` from the site `ftp://ftp.example.com` and you killed the `wget` process by mistake after about 3GB of download. Make sure that your current directory is the one that contains the partially downloaded ISO. Then run the same `wget` command you did originally, adding the `-c` (continue) option as follows:

```
$ wget -c ftp://ftp.example.com/mydvd.iso
```

If you had not used the `-c` option, in this case, a new download would have started using the file name `mydvd.iso.1` to download to.

> **NOTE:** Another command that you might be interested in, similar to `wget`, is the `curl` command. Like `wget`, `curl` can download files using the ftp or http protocols. Curl can also do multiple file transfers on the same connection.

# Using ssh for remote login/remote execution

Although the `telnet` and `rlogin` login commands and `rsh` remote execution command have been around much longer, the `ssh` command is the preferred tool for remote logins and executions. The reason is that `ssh` provides encrypted communication so you can use it securely over insecure, public networks between hosts that don't know each other.
In the following example, `ssh` is being used to log in to a computer named maple. Because no user is specified, `ssh` tries to log in as the current user (which is the root user in this case).

```
# ssh maple
root@maple's password:
```

If you wanted to log in as a different user, you could use the `-l` option. For example, to log in to the computer named maple as the user named jake, you could type the following:

```
# ssh jake@maple
jake@maple's password:
```

The `ssh` command can also be used to execute a command on the remote computer. For example, if you wanted to monitor the messages file on a remote computer for a minute, you could type the following command:

```
# ssh root@maple "tail -f /var/log/messages"
root@maple's password:
```

After you typed the password in the preceding case, the last several lines of the `/var/log/messages` file on the remote computer would be displayed. As messages were received, they would continue to be displayed until you decided to exit (press Ctrl+C to exit the `tail` command).