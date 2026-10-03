The information in these files is put into NIS databases automatically when you create a NIS master server. Other system files can also be managed by NIS if you want to customize your configuration.

NIS makes updating network databases much simpler than with the /etc file system. You no longer have to change the administrative /etc files on every system each time you modify the network environment. For example, if you add a new system to a network running NIS, you only have to update the input file in the master server and run /usr/ccs/bin/make. This process automatically updates the hosts.byname and hosts.byaddr maps. These maps are then transferred to any slave servers and made available to all the domain's client systems and their programs.

Just as you use the cat command to display the contents of a text file, you can use the ypcat command to display the values in a map. Here is the basic ypcat syntax:

```
ypcat [-k] <mapname>
```

If a map is composed only of keys, as in the case of ypservers, use ypcat -k otherwise, ypcat prints blank lines.

In this case, mapname is the name of the map you want to examine.

You can use the ypwhich command to determine which server is the master of a particular map:

```
ypwhich -m <mapname>
```

In this case, mapname is the name of the map whose master you want to find. ypwhich responds by displaying the name of the master server.

These and other NIS commands are covered in the following sections.

# PLANNING YOUR NIS DOMAIN

Before you configure systems as NIS servers or clients, you must plan the NIS domain. Each domain has a domain name, and each system sharing the common set of maps belongs to that domain.