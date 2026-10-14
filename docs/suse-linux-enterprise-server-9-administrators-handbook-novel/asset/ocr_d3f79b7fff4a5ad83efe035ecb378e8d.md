the user. Because the channel is encrypted, the user's data, such as username, password, and so on, is protected from network sniffing. The user can then proceed with system maintenance tasks such as resetting passwords and editing system configuration files, knowing that any information exchanged is secure.

You start sshd as a standalone application through `/etc/init.d` and configure it through files contained within `/etc/ssh`. You can initiate the sshd service at boot time by using the YaST Runlevel Editor (System, Runlevel Editor). Figure 8.9 shows the service as enabled at boot time.

# FIGURE 8.9

Adding sshd to run at boot.

![](bbox=[0.183, 0.346, 0.765, 0.627])

You can connect to a host through ssh using the syntax shown here:

```
Athena> ssh -l eric Hermes.UniversalExport.ca
```

In this example, the -l option is used to specify the login account at the remote end. Without this option, ssh will use the account name associated with the current session to connect. Once you are connected, an encrypted session is established between the hosts. After an exchange of cryptographic information, you will be asked for the password of the remote account. Once the password has been verified, you will have an encrypted terminal connection. Later in this chapter, you will learn how ssh connections can be turned into tunnels for encrypting insecure protocols between hosts.