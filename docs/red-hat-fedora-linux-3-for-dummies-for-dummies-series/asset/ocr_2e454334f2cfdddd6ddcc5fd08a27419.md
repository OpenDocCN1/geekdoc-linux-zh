have become very fast. Because you connect to the Internet, hackers can steal your /etc/passwd file, which contains the encrypted version of your text-based passwords, and then use a computer to crack them.

Don't use any password found in a dictionary. Simple words of any language are easy to crack. For example, don't use the password fedora. Instead, using the words fedora and rocks, you can change e to 3 and o to 0 and then combine them into the good password f3doraR0cks!, which means that the cracking software has to use brute force, which takes longer, rather than a mere dictionary search, to discover it.

# Scan Me

Information is king when it comes to people hacking into systems and keeping them out. Hackers use knowledge about your computer and network to break into your systems. One common and powerful tool for gaining information about which type of operating system you have and the services it runs is nmap. This port-scanning tool can discover a wealth of information about individual computers and networks.

nmap is included in the Fedora Core distribution. To install it, log in as root, mount the DVD (insert it in to the drive), and enter the following command:

```
rpm -ivh /media/cdrom/Fedora/RPMS/nmap*
```

You can then scan yourself, or any computer on your private network (if you have one). If you're logged in to cancun, for example, you can run the nmap localhost command.

The nmap command probes your internal loopback network interface — lo, for example — and returns a list of services you're running. This list shows a sample result:

```
Starting nmap 3.48 ( www.insecure.org/nmap/ ) at 2004-10-19

Interesting ports on localhost.localdomain (127.0.0.1):
(The ports scanned but not shown below are in state: closed)
   Port      State    Service
   22/tcp    open     ssh
   25/tcp    open     smtp
   80/tcp    open     http
   111/tcp   open     rpcbind
   631/tcp   open     ipp
   6000/tcp  open     http-alt

Nmap run completed -- 1 IP address (1 host up) scanned
```