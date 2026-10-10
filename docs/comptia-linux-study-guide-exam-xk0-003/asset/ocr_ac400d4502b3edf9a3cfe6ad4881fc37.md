# ### Configuring the Root Zone

Performing a full recursive lookup requires that your system have an accurate root zone record. This is normally installed along with BIND and is referenced by the zone `"."` section of *named.conf* (which does not appear in Listing 10.2):

```
zone "." IN {
    type hint;
    file "named.ca";
};
```

These lines define a *DNS zone*—that is, a set of addresses that the server can resolve using rules defined elsewhere. The `"."` zone is also known as the *root zone*—this is the entire Internet namespace. This zone is defined by the *named.ca* file, which is located in the directory defined by the *directory* line in the *options* section of *named.conf*—normally `/var/named`. You shouldn’t ordinarily change this particular definition, since it’s normally the same for all DNS servers that use the Internet’s DNS. If your system is configured to forward DNS requests, as described earlier in “Setting Overall BIND Options,” the root zone definition is optional.

If the root servers ever change (as they do from time to time), your existing configuration might not work. You can retrieve the current root zone file in various ways. One is to type the following command:

```
$ dig @a.root-servers.net . ns > db.cacbe
```

Alternatively, you can download db.cacbe from *ftp://ftp.internic.net/domain/*. (Note that this is an FTP site, not a Web site. Chapter 11 provides some pointers on using FTP clients.) Once you’ve retrieved the latest zone file, you can replace the old one (*named.ca* in the preceding example; the filename you retrieve may not match what’s used on your system) with the new file.

# ## Configuring a Domain with BIND

On a small local network (say, one with a dozen or so computers), you can set up each computer with an `/etc/hosts` file for hostname resolution, as described in Chapter 8. This approach works, but it becomes tedious as the number of *computers* grows; every time you add a computer or change its IP address, you must change the `/etc/hosts` file for *every* computer on the network. Rather than deal with this hassle, you may want to configure a DNS server to handle local hostnames. Doing so requires making three sets of changes: adding a zone reference to `/etc/named.conf`, creating a forward zone file, and creating a reverse zone file.

# ## Adding a Zone Reference to the Main BIND Configuration File

A default `/etc/named.conf` file usually includes one or more zone file references, such as the one to the root zone presented earlier. These references begin with the keyword *zone*, include the name of the domain to be managed, and link to a zone file in another directory (normally `/var/named`).