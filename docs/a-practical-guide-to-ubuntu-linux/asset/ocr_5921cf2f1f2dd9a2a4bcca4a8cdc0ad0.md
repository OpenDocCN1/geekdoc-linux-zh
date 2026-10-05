# 18

# IN THIS CHAPTER

+   Introduction to OpenSSH ....... 664
Running the ssh, scp, and sftp OpenSSH Clients ...... 667
JumpStart: Using ssh and scp to Connect to an OpenSSH Server...... 667
Setting Up an OpenSSH Server (sshd) ........ 676
JumpStart: Starting an OpenSSH Server...... 677
Troubleshooting .................................... 680
Tunneling/Port Forwarding....... 681

OpenSSH is a suite of secure network connectivity tools that replace telnet/telnetd, rcp, rsh/rshd, login/logind, and ftp/ftpd. Unlike the tools they replace, OpenSSH tools encrypt all traffic, including passwords. In this way they thwart malicious users who attempt eavesdrop, hijack connections, and steal passwords.

This chapter covers the following OpenSSH tools:

+   - scp—Copies files from one to another system
- sftp—Copies files to and from other systems (a secure replacement for ftp)
- ssh—Runs a command on or logs in on another system
- sshd—The OpenSSH daemon (runs on the server)
- ssh-keygen—Creates, manages, and converts RSA for DSA host/user authentication keys