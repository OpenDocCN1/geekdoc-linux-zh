Compression Compression, which is enabled with the `-C` option, can speed up communication over a low-bandwidth connection. This option is commonly used with port forwarding. Compression can increase latency to an extent that may not be desirable for an X session forwarded over a high-bandwidth connection.

# # CHAPTER SUMMARY

OpenSSH is a suite of secure network connectivity tools that encrypts all traffic, including passwords, thereby thwarting malicious users who might otherwise eavesdrop, hijack connections, and steal passwords. The components discussed in this chapter are `sshd` (the server daemon), `ssh` (runs a command on or logs in on another system), `scp` (copies files to/from another system), `sftp` (securely replaces ftp), and `ssh-keygen` (creates authentication keys).

To ensure secure communications, when an OpenSSH client opens a connection, it first verifies that it is connected to the correct server. Then OpenSSH encrypts communication between the systems. Finally OpenSSH makes sure that the user is authorized to log in on or copy files from/to the server.

OpenSSH also enables secure X11 forwarding. With this feature, you can run securely a graphical program on a remote system and have the display appear on the local system.

# # EXERCISES

+   1. What is the difference between the `scp` and `sftp` utilities?
+   2. How can you use `ssh` to find out who is logged in on a remote system?
+   3. How would you use `scp` to copy your `~/.bashrc` file from **bravo** to the local system?
+   4. How would you use `ssh` to run **xterm** on **bravo** and show the display on the local system?
+   5. What problem can enabling compression present when using `ssh` to run remote X11 applications on a local display?
+   6. When you try to connect to another system using an OpenSSH client and you see a message warning you that the remote host identification has changed, what has happened? What should you do?