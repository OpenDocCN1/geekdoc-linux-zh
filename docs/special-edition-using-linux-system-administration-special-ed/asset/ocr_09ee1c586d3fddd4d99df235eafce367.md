```
```text
method timehash {
    newsgroups: alt.binaries.*
    class: 0
    size: 0,1000000
}
method timehash {
    newsgroups: *
    class: 2
}
```
```

For timehash methods, storage class IDs (indicated in the class parameter) are used to store articles in separate directory trees so that different expiration policies can be applied to each storage class. The newsgroups must be divided based on retention time of articles in those groups, and a storage class created for each collection. The storage class IDs that are assigned are used in the expire.ctl file to control expiration of articles.

# ## USING THE overview.ctl FILE WITH CNFS AND timehash STORAGE

The overview.ctl file determines where article overview information will be stored for each newsgroup. Overview information is stored in one or more storage files identified by unique numbers between 0 and 254. Each line consists of the storage file number followed by a single colon and a wildcard pattern list of which newsgroups are to be stored in that file. As with storage.conf, the first matching line is used to determine where to store overview information for a given article.

The goal is to spread the overview files across a number of smaller files rather than one large file. One suggested method is to create 27 storage areas; the first 26 will be for newsgroups a* through z*, and the 27th will be for * to catch all articles which fail to match the alphabetic wildcard patterns in the first 26 entries. The layout can be modified later by editing the overview.ctl file and running expire. The overview data will be rearranged during the expiration process.

# ## CONTROLLING CLIENT ACCESS WITH THE nnrp.access

The nnrp.access file controls who can access the news server as a reader using a news client. Consider the following nnrp.access file:

```
```text
stdin:RP::*
localhost:RP::*
127.0.0.1:RP::*
*.bwc.org:RP::*
192.115.144.*:RP::*
```
```

Each line in the file takes the following format:

```
```text
<host>:<access privileges>:<username>:<password>:<newsgroups>
```
```

These five fields are used as follows:

+   - The host field can be a hostname (as in line 2 in the example), an IP address (as in line 3 in the example), an IP address range or a wildcard pattern (as in the last line in the example). The field specifies to which host or hosts the rule applies.