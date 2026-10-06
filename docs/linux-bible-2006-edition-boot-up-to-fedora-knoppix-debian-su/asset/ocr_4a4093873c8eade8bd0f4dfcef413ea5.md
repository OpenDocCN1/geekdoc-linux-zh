# 228 Part II ♦ Running the Show

Once you have opened a port in your firewall so others can request a service, then started that service to handle requests, SELinux can be used to set up walls around that service. As a result, this daemon process, configuration files, and data can't access resources they are not specifically allowed to access. The rest of your computer, then, is safer.

Red Hat continues to work out the kinks in SELinux, there have been a tendency for users to see SELinux failures and just disable the entire SELinux service. However, a better course is to find out if SELinux is really stopping you from doing something that is unsafe. If it turns out to be a bug with SELinux, file a bug report and help make the service better.

If you are enabling FTP, Web (HTTP), DNS, NFS, NIS, or Samba services on your Fedora or RHEL system, you should consider SELinux enabled and working with the settings from the Security Level Configuration window to configure those services. For information on SELinux that is specific to Apache Web servers, refer to this website:

```
http://fedora.redhat.com/docs/selinux-apache-fc3.
```

An FAQ on SELinux for Fedora is available here:

```
http://fedora.redhat.com/docs/selinux-faq-fc3.
```

# Protecting Web Servers with Certificates and Encryption

Previous sections told you how to lock the doors to your Fedora system to deny access to crackers. The best dead bolt lock, is useless if you are mugged in your own driveway and your keys stolen. Likewise, the best computer security can be for if you are sending passwords and other critical data unprotected across the Internet.

A savvy cracker can use a tool called a protocol analyzer or a network sniffer to peek at the data flowing across a network and pick out passwords, credit card data, and other juicy bits of information. The cracker does this by breaking into a poorly protected system on the same network and running software, or by gaining physical access to the same network and plugging in his or her own equipment.

You can combat this sort of theft by using encryption. The two main types of encryption in use today are symmetric cryptography and public-key cryptography.

# Symmetric Cryptography

Symmetric cryptography, also called private-key cryptography, uses a single key to both encrypt and decrypt a message. This method is generally inappropriate for securing data that will be used by a third party, because of the complexity of secure