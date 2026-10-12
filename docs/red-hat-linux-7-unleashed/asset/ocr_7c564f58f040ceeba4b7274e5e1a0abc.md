The Network Information Service (NIS) is a simple, generic client/server database system. Under Linux, however, the most common use for it is sharing password and group files across a network. This chapter covers the setup of both master and slave NIS servers, as well as the configuration needed for clients to use them.

NIS, developed by Sun Microsystems as part of its SunOS operating system, was originally known as The Yellow Pages, or YP for short. Unfortunately, the name Yellow Pages had already been trademarked, and the resulting lawsuit forced the name change to NIS. You will soon discover that all the NIS commands are still prefixed with yp.

The NIS protocol was made public and implementations of it quickly spread to other variations of UNIX. Linux has supported NIS from its onset. Because Linux follows the NIS standard, it can work with other flavors of UNIX as either the NIS server or client.

# ## Understanding NIS

As you configure your network, you will find that some of your configuration files are not host specific, but they require frequent updating. `/etc/passwd` and `/etc/group` are two that come to mind. NIS enables you to set up a master server where these files are stored and then configure each machine on your network as clients to this server. Whenever a client needs to fetch an entry from the `/etc/passwd` file, it consults the NIS server instead.

Two prerequisites must be met in order for a file to be shareable via NIS. First, the file must be tabular with at least one entry that is unique across the entire file. In the `/etc/passwd` file, this entry is either the login or UID. Second, the file in its raw form must be a straight text file.

With the criteria met, the files are converted into DBM files, a simple database format allowing for quick searches. You must create a separate DBM for each key to be searched. In the `/etc/passwd` file, for instance, you need the database to be searchable by login and by UID. The result is two DBM files, `passwd.byname` and `passwd.byuid`.

The original text file, along with the DBM files created from it, is maintained at the NIS master server. Clients that connect to the server to obtain information do not cache any returned results.

# ## NIS Domains

NIS servers and clients must be in the same NIS domain to communicate with one another. Note that the NIS domain is not the same as a DNS domain, although it is valid for them to share the same name.