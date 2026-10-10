# Chapter 6 - Kali Linux Installation

Kali Linux can be installed on a hard disk like any GNU / Linux distribution, it can also be installed and configured to perform a dual boot with a Windows Operating System, in the same way, it can be installed on a USB drive, or installed on an encrypted disk

It is suggested to review the detailed information on the various installation options for Kali Linux, on the following page: [http://docs.kali.org/category/installation](http://docs.kali.org/category/installation)

# Change Root Password

For a good security practice, it is recommended to change the default password assigned to the root user. This will make it difficult for malicious users to access the system with this default password.

```
# passwd root
Enter new UNIX password:
Retype new UNIX password:
```

> [\*] The password will not be displayed as long as it is written and must be entered twice.

# Starting Network Services

Kali Linux network services are, HTTP, Mestaploit, MySQL, OpenVAS, and SSH.

If the HTTP service is required to start, the following command must be executed:
```text
#/etc/init.d/apache2 start
```

These services can also be started and stopped from the menu: Applications -> Kali Linux -> System Services.

Kali Linux provides official documentation on several of its aspects and features. The documentation is in constant work and