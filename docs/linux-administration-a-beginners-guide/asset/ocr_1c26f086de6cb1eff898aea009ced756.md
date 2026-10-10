The first tool, **ypcat**, dumps the contents of an NIS map. This is useful for scripts that need to pull information out of **NIS**. *ypcat* can pull the entire map down, and then *grep* can be used to find a specific entry. The *ypcat* command is also useful for simple testing of services, as demonstrated earlier in this chapter.

The **ypwhich** command returns the name of the NIS server that is answering your requests. This is also a good diagnosis tool if *NIS* doesn't appear to be working as expected. For example, let's say you've made a change in the master NIS tables, but your change can't be seen by a specific client. You can use *ypwhich* to see which server the client is bound to. If it's bound to a secondary server, it might be that the secondary server is not listed in the primary server's *var/yp/ypservers* file.

An example of **ypwhich** usage is as follows:

```
[root@ford /root]# ypwhich
```

The **ypmatch** command is a close relative of *ypcat*. Rather than pulling an entire map down, however, you supply a key value to *ypmatch* and only the entry correspond-ing to that key is pulled down. Using the *passwd* map as an example, I can pull down the entry to sshask with this simple command:

```
[root@ford /root]# ypmatch sshask passwd
```

# USING NIS IN CONFIGURATION FILES

One of the most popular uses of NIS is the sharing of the*/etc/passwd* file so that everyone can log in to all hosts on the network by making a single modification to the master*/etc/passwd* map. Some distributions of Linux automatically support this feature once they see NIS running. Others still require explicit settings in*/etc/passwd* so that the login program knows to check NIS as well as the base password file.

> NOTE: Whether a system automatically uses NIS for login depends on which C library the system uses. The newer glibc-based distributions (such as Red Hat and Caldera) automatically use NIS, whereas libc5-based versions (such as Debian) do not. Not all distributions have settled on one library or another, and the subject is a hot topic of debate. With libc5 development stopped, however, it's inevitable that all distributions will use glibc.

Let's assume that you need to add the special tokens to your*/etc/passwd* file to allow logins from users listed in the NIS passwd file.

Here is the base setting you should add to your client's*/etc/passwd* file to allow host login for all users listed in the NIS passwd list:

```
*:::::::
```