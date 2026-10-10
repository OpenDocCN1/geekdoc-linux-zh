# # DNS Configuration

Under Linux, the **named** program provides DNS. This program is usually started at boot time by specifying that Internet domain name server (**named**) should be activated. (You can do this using COAS.)

**named** reads a configuration file called `(/etc/named.conf)`, any other files specified by that file, and then listens for DNS queries. **named** is part of the BIND (Berkeley Internet Name Daemon) distribution. In addition to the manual page named(8), you can look at the `/usr/doc/bind-8.1./html1/index.html` with a Web browser for more details. (We'll refer to this as the HTML documentation.)

The file `(/etc/named.conf)` is the master configuration file for **named**.

> **Background Material**
> 
> If you have use an old version of **named**, the old `(/etc/named.boot)` file is no longer used. The new configuration file is in a different format; the program **named-bootconf** will convert a **named.boot** file into a **named.conf** file.

The **named.conf** file has many options; we'll just cover the most frequently used ones here. Read the HTML documentation for all the details.

# ## Options

The **options** statement sets up global options for **named**. There are many options; some of them are as follows:

+   * **directory** Specifies the directory for remaining configuration files. **named** uses many auxiliary configuration files; any relative pathnames are assumed to be relative to the directory specified with this option.

+   * **recursion** This option can be either *yes* or *no*. If it is *yes* (the default), then the name server does all the work of looking up a name. If it is *no*, then the name server or simply refers the client to an authoritative name server if it does not have the information itself. (See Figure 12.1.)

+   * **forwarders** This option can be used to forward queries to other name servers. For example, in a large organization, each departmental name server can forward queries to a central name server. The central name server can quickly build up a rich cache of information, greatly reducing the need to perform name queries outside the organization (and presumably over a slow link). The **forwarders** option takes a list of IP addresses.