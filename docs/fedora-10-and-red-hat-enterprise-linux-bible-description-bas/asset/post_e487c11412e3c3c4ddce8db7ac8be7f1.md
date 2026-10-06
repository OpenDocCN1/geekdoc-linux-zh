
What exactly is a port number? It is a unique number that has been set aside for a particular network service. It allows network connections to be properly routed to the software that handles that service. For example, when an e-mail message is delivered from some other computer to your Linux box, the remote system must first establish a network connection with your system. Your computer receives the connection request, examines it, sees it labeled for port 25, and knows that the connection should be handed to the program that handles mail (which happens to be sendmail).

I mentioned that SMTP uses the TCP protocol. Some services use UDP, the User Datagram Protocol. All you really need to know (for the purpose of this security discussion) is that TCP and UDP provide different ways of packaging the information sent over a network connection. A TCP connection provides error detection and retransmission of lost data. UDP doesn't check to ensure that the data arrived complete and intact; it is meant as a fast way to send non-critical information.

## Disabling network services

Although there are hundreds of services (listed in /etc/services) that potentially be available and subject to attack on your Fedora or Red Hat Enterprise Linux system, in reality only a few dozen are installed and only active by default. Most network services are enabled by the xinetd process or by a start-script in the /etc/init.d directory.

xinetd is a daemon that listens on a great number of network port numbers. When a connection is made to a particular port number, xinetd automatically starts the appropriate program for that service and handles the connection to it. The xinetd daemon improves on its predecessor, inetd, by offering features that include more flexible access control, more logging settings, and denial-of-service prevention.

The configuration file /etc/xinetd.conf is used to provide default settings for the xinetd server. The directory /etc/xinetd.d contains files telling xinetd what ports to listen on and what programs to start. Each file contains configuration for a single service, and the file is usually named after the service it configures. For example, to enable the rsync service, use the rsync file in the /etc/xinetd.d directory and look for a section similar to the following:

```
service rsync
{
    disable = yes
    socket_type = stream
    wait = no
    user = root
    server = /usr/bin/rsync
    server_args = --daemon
    log_on_failure += USERID
}
```

Note that the first line of this example identifies the service as rsync. This exactly matches the service name listed in the /etc/services file, causing the service to listen on port 873 for TCP and UDP protocols. You can see that the service is off by default (disable = yes). To enable rsync, change the line to read like this:

```
disable = no
```

> TIP: The rsync service is a nice to turn on if your machine is an FTP server. It allows people to use an rsync client (which includes a checksum-search algorithm) to download files from your server. With that feature, users can restart a disrupted download without having to start from the beginning.

Because most services are disabled by default, your computer is only as secure as you make it. You can double-check that insecure services, such as login and rsh (which are included in the rsh package), are also disabled by making sure that disabled = yes is set in the /etc/xinetd.d/login and rsh files.

> TIP: You can make the login service active but disable the /etc/host.equiv and .rhosts files, requiring login to always prompt for a password. Without disabling the service, locate the server in the rsh file (server = /usr/sbin/in.rsh) and add a follow by -L at the end. Of course, that doesn't change the fact that your password and data will still be sent encrypted over the network.

You need to send a signal to the xinetd process to tell it reload its configuration file. The quickest way to do that is to reload the xinetd service. As the root user, type the following from a shell:

```
# service xinetd reload
Reloading configuration:      [ OK ]
```

That's it — you have enabled rsync service. Provided that you have properly configured your FTP server (Chapter 19), clients should now be able to download files from your computer via the rsync protocol and be able to restart interrupted downloads.

## Securing services with SELinux

Red Hat, Inc. did a clever thing when it took its first step at implementing SELinux in Red Hat systems. Instead of creating policies to control every aspect of your Linux system, it created a "targeted" policy that focused on securing those services that are most vulnerable to attacks. Red Hat then set about securing services in such a way that, if they were compromised, a compromise couldn't compromise the rest of the system as well.

After you opened a port in your firewall so others can request a service, and started that service to handle requests, SELinux can be used to set up walls around that service. As a result, its daemon process, configuration files, and data can't access resources that are not specifically allowed to access. The rest of your computer, is, safer.

## Part III: Administering Fedora and RHEL

Red Hat continues to work out the kinks in SELinux, there has been a tendency for users to experience SELinux failures and just disable SELinux. If you tried SELinux in the past and turned it off when you had a problem, consider that SELinux has improved quite a bit in recent versions and it might be time to try it again.

If you encounter a failure related to SELinux, try to find out if SELinux should caused the failure. In other words, maybe you were doing something that was unsafe. However, if the failure you encounter is a bug with SELinux, file a bug report to http://jira.redhat.com and help make the service better.

See Chapter 10 for a more in-depth description of SELinux.

## Protecting Web servers with certificates and encryption

Previous sections told you how to lock the doors to the Fedora or RHEL system to deny access to crackers. The worst dead bolt lock, however, is useless if you are mugged in your driveway and your keys stolen. Likewise, better security can be for naught if you are sending passwords and other critical data unprotected over the Internet.

A savvy cracker can use a tool called a protocol analyzer or network sniffer to peek at the data flowing across a network and pick out passwords, credit card data, and other bits of information. The cracker does this by breaking into a poorly protected system on the same network and running software, or by gaining physical access to the same network and plugging in his or her equipment.

You can combat this sort of theft by using encryption. The two main types of encryption in today are symmetric cryptography and public-key cryptography.

### Symmetric cryptography

Symmetric cryptography, also called private-key cryptography, uses a single key to both encrypt and decrypt a message. This method is generally inappropriate for securing data that will be used by a third party, because of the complexity of secure key exchange. Symmetric cryptography is generally useful for encrypting data for one's own purposes.

A classic use of symmetric cryptography is for a personal password vault. Anyone who has been using the Internet for any amount of time has accumulated a quantity of user names and passwords for accessing various sites and resources. A personal password vault lets you store this information in an encrypted format. The end result is that you have to remember one password to unlock all of your access information.

Until recently, the United States government was standardized on a symmetric encryption algorithm called DES (Data Encryption Standard) to secure important information. Because there is no direct way to crack DES-encrypted data, to decrypt DES encrypted data without a password you would have to use an unimaginable amount of computing power to try to guess the password. This is also known as the brute force method of decryption.
