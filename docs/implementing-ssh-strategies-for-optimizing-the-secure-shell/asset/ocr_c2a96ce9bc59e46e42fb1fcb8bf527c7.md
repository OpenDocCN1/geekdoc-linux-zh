Similar to SecureCRT, OpenSSH's command-line client can be used to use SSH via HTTP proxy servers. Unlike with SecureCRT, you will need to download a tool called Corkscrew, written by Pat Padgett, from www.agromann.net/ corkscrew. Once you have downloaded the tool to `/usr/local/bin`, enter the following commands to enable Corkscrew, which will help you use SSH through HTTP proxy servers:

Unzip and install the utility.

```
#gunzip -c corkscrew-2.0.tar.gz | tar xvf -
#cd corkscrew-2.0
#./configure
#make
#make install
```

Edit your `~/ssh/config` file and add the following lines, replacing "http.proxy.server" with the hostname or IP address of your HTTP proxy server and "port" with the port, usually 80 or 8080, that your HTTP proxy server is listening on.

```
ProxyCommand /usr/local/bin/corkscrew http.proxy.server port $h $p
```

Use the `--F` flag to connect to the remote SSH server.

```
#ssh -F config ip.ssh.server -p 80
```

That's it! You will now be able to use OpenSSH's command-line client through HTTP proxy servers to reach SSH servers.

# Securing Wireless Networks with SSH

Wireless connections, specifically 802.11b, have been plagued with security issues almost since their introduction. From serious security issues with WEP, to clear-text communication of management beacons, wireless technology is a key target for attackers. Nevertheless, wireless technology is a "must-have" in many organizations. If your organization will not deploy wireless technology due to its security issues, someone who is unauthorized may deploy it for you, which probably won't be done in a secure fashion. You will be examining how to use your previous SSH and proxy model to secure wireless networks. Keep in mind that you can already secure other protocols, such as mail (POP3 and SMTP) and file transfer (FTP, SMB, NFS), with port forwarding over wireless networks. The following sections discuss how to use port forwarding to secure Web traffic over wireless networks.