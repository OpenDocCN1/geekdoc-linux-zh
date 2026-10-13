# # About DNS

You might not be familiar with DNS, but if you’ve ever surfed the Internet, you’ve made extensive use of it. Computers know how to find each other by means of their addresses, and specifically by an IP address, just as you can (usually) find the book store after looking up its address in the phone book. DNS is to computers what the phone book is to you. You don’t remember Internet sites by their IP addresses, but by their names. But you don’t know where the FOOBAZ bookstore is if you’ve never been there (or seen it in passing), so you need to look up the address. Similarly, when you want your Web browser to find www.cadlerasystems.com, your system uses DNS to look up the IP address.

On your Linux system you have resolver libraries that know how to resolve names into IP addresses. In your /etc/nsswitch.conf (name service switch configuration) file you have a line that looks like the following:

```
hosts:        files dns
```

This line tells the resolver routines that when they are looking for hosts, they need to first consult the system’s files, and if they don’t find what they’re looking for there, they need to perform a DNS lookup.

> > **Note**
> >
> > The nsswitch.conf file replaced the /etc/host.conf file when Linux moved from libc5-based systems to the new glibc (libc6). The nsswitch.conf file follows Sun Microsystems’s lead and acts as a single reference for system database files for applications requiring this information.

The system files start with /etc/hosts, where commonly accessed local network hosts might be listed. This lookup is faster than a DNS lookup. But if names that might change are included, you might wonder why the lookup failed to find what you were looking for. Therefore, refrain from putting any entries over which you have no control into /etc/hosts.

The resolver libraries, failing to find the address they seek in /etc/hosts, consult /etc/resolv.conf to find the IP addresses of machines known as Domain Name Servers, or name servers for short. Up to three, but not fewer than two, need to be entered in this file. Why two? In case one is down. But no more than three are consulted, so all name server entries beyond the first three are ignored.

> > **Note**
> >
> > If you run your own name server, you’ll want to make sure all your hosts point to your name server first. The host the name server is running on should point to 127.0.0.1 for name resolution.