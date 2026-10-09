What do you think of when you hear the term system configuration? If you were to pose that exact same question to a group of people, you would, most likely, get entirely different responses. System configuration encompasses such a broad area of system administration that it is very difficult to cover all aspects. And so, we will concentrate on configuration related to users and login, hardware, booting up and startup services, networking, and security. Even though there are numerous applications that will allow you to manipulate system configuration through a graphical interface, you will have better control of the system if you know where the configuration information is stored and how to modify it manually when necessary.

Depending on the operating system, the configuration information is stored in different locations. For example, Microsoft Windows stores most configuration data in the Registry, while the Mac OS stores it in separate binary files in a special Preferences folder. How about Linux? Where does it store the configuration details? For the most part, Linux, by which I mean the core components as well as individual applications, stores the information in plain text files in the /etc directory or in one of its subdirectories. This gives us a number of advantages over the other operating systems, namely:

+   - We can read and edit the information easily with an text editor.
+   - We can back up the files consistently.
+   - We can maintain version control, thereby keeping track of all changes.

Unfortunately, since each component or application stores its configuration information individually in a separate file, there are bound to be differences in syntax between them. However, a majority of the files have a syntax that is easy to understand, as you will see in a moment.

# ## Example: Finding the DNS Server

For example, perhaps you entered a DNS server address when you were installing the operating system back in Chapter 1. That DNS server address forms part of the system’s configuration, and its value is stored in the appropriate configuration file under the /etc directory hierarchy.

If you take a look at the /etc directory, you’ll see that there are quite a lot of configuration files there. Which one contains DNS server configuration? If you know the DNS server address, then one way to find out is to use the grep command to search for the file that contains that address. For example, if you used the primary nameserver address 192.168.1.1, then you can find the correct configuration file via the following command:

```
# grep -ri 192.168.1.1 /etc
/etc/resolv.conf:nameserver 192.168.1.1
```