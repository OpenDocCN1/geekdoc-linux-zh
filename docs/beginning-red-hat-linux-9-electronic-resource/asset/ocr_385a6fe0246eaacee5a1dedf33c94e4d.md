You can also customize the firewall rules within these different levels of security. Red Hat Linux allows you to select the trusted devices – network interfaces that are expected to carry traffic from sources that you can trust blindly. In a home network this would generally be the interface card connected to the rest of your home network. You should definitely not mark your Internet interfaces as trusted, unless you are absolutely sure about your security needs.

Apart from these devices, this screen also allows you to specify network services that external network identities will be able to access from your computer. To be on the safe side, select only the services that you actually expect to be used, and that do not have insecure software behind them. For example:

+   -   SSH (Secure Shell) allows you to work on a remote machine while ensuring that the data exchanged in the process is kept encrypted and secure. It is generally safe for SSH servers to be open; indeed, this is recommended if you want to be able to access your computer from other machines.

+   -   If you want to use this machine to receive mails from others, you may choose to have an SMTP server on your machine receive these mails. In this case you should allow incoming connections to the SMTP server.

+   -   Many FTP servers have had a long history of insecurities. It is advisable to leave incoming connections to such FTP services closed, and open them up in the firewall only when you need them. When you've finished, you should immediately cut off their access using the firewall.

# Setting Additional Language Support

If you're expecting to use multiple languages, you can select them in the next screen:

![](bbox=[0.2, 0.64, 0.77, 0.93])