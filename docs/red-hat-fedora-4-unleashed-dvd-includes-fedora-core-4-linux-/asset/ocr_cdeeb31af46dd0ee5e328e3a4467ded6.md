can cause premature article expiration, depending on the size of the buffer file. Most news administrators who use this method learn by trial and error the buffer file size necessary to handle the standard news traffic load at their sites.

> **CAUTION**
> If a newsgroup is not covered by a specific storage method, INN doesn't store the articles received for that newsgroup, and it produces an error message for each article. This can have a devastating effect on the news server. For a simple news server, it is best to select a single method of storage and configure the storage.conf file to use that method for all the newsgroups.

By default, the Fedora Core /etc/news/storage.conf file doesn't define any default storage method, but it is fully configured and commented out. You must define at least one method to use for INN to work properly; to do so, you can simply uncomment the desired section.

# The readers.conf File

You use the /etc/news/readers.conf configuration file to define permissions for newsreaders that use your news server. If you are allowing your local users to connect to your news server to read articles, you must configure the readers.conf file to support them.

The readers.conf file consists of the following three types of data:

+   * An authentication definition
+   * An access definition
+   * Parameters and values

The authentication definition defines categories of users who will be accessing your news server. You can create several categories of users, based on various factors, such as remote address, newsgroups accessed, and type of authentication method used. The syntax of the authentication section is as follows:

```
auth name {
    hosts: hostlist
    auth: auth-program
    res: res-program
    default: defuser
    default-domain: defdomain
}

```

The name value is used as a label to uniquely identify the authentication definition. The authentication definition uses parameters and values to identify its actions. The hosts parameter uses the hostlist value to identify individual remote hosts covered by the authentication definition. These can be listed by using either hostnames or numeric IP addresses, along with matching wildcard characters.