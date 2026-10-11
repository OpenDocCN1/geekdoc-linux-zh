# # Using TCP Wrappers to Secure a Service

Though covered in detail elsewhere, TCP wrappers are an important part of system security and require a quick review.

The majority of system services or daemons use the **libwrap** library for TCP wrappers functionality. The concept of TCP wrappers is to use a set of allow and deny files that wrap daemons in a protective sheath that keeps unwanted hosts from even contacting the daemon. TCP wrappers cannot protect from a host that is spoofing itself as a known or permitted host—that is where usernames, passwords, and other security measures come into play.

Remember that TCP wrappers depend on the `/etc/hosts.allow` and `/etc/hosts.deny` files for configuration. If a host or an address should be permitted to contact a service, an entry can be placed in the `/etc/hosts.allow` file to specifically allow that host to contact the service, or you can just leave the service open and not wrap it with protection.

It’s when you have a more complex set of rules or policies that mandate that some hosts have access to particular services or that some other hosts don’t have access that the real utility of using both an allow and a deny file becomes apparent.

![](bbox=[0.09, 0.57, 0.18, 0.67])

> Keep in mind that any host you permit to have access in the `/etc/hosts.allow` file will have access, regardless of what entries are in the `/etc/hosts.deny` file!

# ## Allow and Deny Files

The syntax used in the `/etc/hosts.allow` and `/etc/hosts.deny` files is fairly simple. For example, to deny access to all services from all hosts but the machine Mortimer, you would use an `/etc/hosts.allow` file with the following entry:

```
ALL: mortimer.example.com
```

Then in the `/etc/hosts.deny` file, you would have this entry:

```
ALL: ALL
```

Take care to plan out what is the most common rule for access to the system being configured: Is it a mostly open system or a mostly closed system? If the system is a mostly open one, you’d effectively reverse the previous setup,