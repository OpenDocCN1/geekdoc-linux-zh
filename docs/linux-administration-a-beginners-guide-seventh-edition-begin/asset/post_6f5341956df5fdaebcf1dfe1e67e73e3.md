
## CHAPTER 16 Domain Name System (DNS)

### Downloading, Compiling, and Installing the BIND Software from Source

If ISC BIND software is not available in prepackaged format for your particular distribution, you can always build the software from source code available from the ISC site at http://isc.org. You might also want to take advantage of the most recent fixes available for the software, which your distribution may not have implemented. As of this writing, the current stable version of the software is 9.10.3, which can be downloaded from:

http://ftp.isc.org/bind/9.10.3/bind-9.10.3.tar.gz

Make sure that you have the openssl-dev package installed on your RPM-based distribution before attempting to compile. The equivalent package in Debian/Ubuntu is libssl-dev. This package ensures that you have the necessary header files to support some of the advanced features of BIND. Once the package is downloaded, unpack the software as shown. For example, we downloaded it into the /usr/local/src/ directory. Unpack the tarball then:

```bash
tar xvzf bind-9.10.3.tar.gz
```

Change to the bind subdirectory created by the preceding command. And take a minute to study all README(s) that may be present. Next configure your binding with the configure command. Assuming you want BIND to be installed under the /usr/local/named/ directory, you will run this:

```bash
./configure --prefix=/usr/local/named
```

To compile and install bind under the commands specified by the prefix, issue these commands:

```bash
make; make install
```

The version of BIND software that we built from source installs the server daemon (named) and some other useful utilities under the /sbin/ directory. The client-side programs (dig, host, nsupdate, and so on) are installed under the /bin/ directory.

### What Was Installed

Many programs come with the main bind and bind-utils packages that were installed during the package manager. We are interested in the following tools:

- /usr/local/named/named The DNS server program itself.
- /usr/local/named/sbin/rndc The bind name server control utility.
- /usr/local/named/bin/host A program performs a simple query on name server.
- /usr/local/named/bin/dig A program that performs complex queries on name server.

The remainder of the chapter will discuss some of the programs/utilities listed here as well as their configuration and usage.

### Understanding the BIND Configuration File

The named.conf file is the main configuration file for BIND. Based on this file's specifications, BIND determines how it should behave and what configuration files, if any, must be read. This section covers what you need to set up a general-purpose DNS server. You'll find a complete guide to the new file format in BIND's documentation. The general format of the named.conf file is follows:

```bind
statement {
    // comments
}
```

The statement keyword tells BIND we're about to describe a particular facet of its operation, and options applying to that statement. The curly braces are required so that BIND knows which options are related to which statements; a semicolon follows every option and after the closing curly brace. example of this follows:

```bind
options {
    directory "/var/named"; // put config files in /var/named
}
```

This means that this is an option statement. The particular option here is the directive that specifies BIND's working directory—that is, the directory on the local system that will hold the name server's configuration data.

### The Specifics

This section documents many comments you will see in a typical named.conf file. The best way to tackle this is to skim it first, and then treat it as a reference for later sections. If some of the directives seem bizarre or don't make sense during your first pass, don't worry. Once you see them in use later, the hows and whys will quickly fall into place.

### Comments

Comments can be in one of the following formats:

| Format | Indicates |
| :--- | :--- |
| // | C++-style comments |
| /*...*/ | C-style comments |
| # | Perl and UNIX shell-style comments |

In the case of the first and last styles (C++ and Perl/UNIX shell), one comment begins, it continues until the end of the line. In regular C-style comments, the commenting /* is required to indicate the end of a comment. This makes C-style comments easier for multiline comments. However, you can pick the comment format that you like and stick with it. No one style is better than another.

### Statement Keywords

The following are some of the most frequently used statement keywords:

| Keyword | Description |
| :--- | :--- |
| acl | Access Control List—determines what kind of access others have to your DNS server |
| include | Allows you to include another file and have that file treated as part of the named.conf file |
| logging | Specifies what information gets logged and what gets ignored. For logged information, you can also specify where the information is logged. |
| options | Addresses global server configuration issues. |
| controls | Allows you to control channels for use by the rndc utility. |
| server | Sets server-specific configuration options. |
| zone | Defines a DNS zone. |

We discuss four of the most often used keywords (include, logging, server, and zone) in more detail in the next sections.

**The include Statement** If you find that your configuration file is starting to grow unwieldy, you may want to consider breaking the file into smaller components. Each file can be included inside the named.conf file. Note that you cannot use the include statement inside another statement.

Here's an example of an include statement:

```bind
include "/path/to/filename_to_be_included";
```

> NOTE All you C and C++ programmers out there: Be sure not to begin include lines with the pound symbol (#), despite what your instincts tell you! That symbol is used to start comments in the named.conf file.

**The logging Statement** The logging statement is used to specify what information you want and where. When this statement is used in conjunction with the syslog facility, you get an extremely powerful and configurable logging system. The items logged are a number of statistics about the status of named. By default, they are logged to the /var/log/messages file. In its simplest form, the various types of logs have been grouped by predefined categories or channels; for example, there are categories for security-related logs, a general category, a resolver category, a queries category, and so on.

Unfortunately, the configurability of this logging statement comes at the price of some complexity, but the default setting is good enough for most users. Here is a simple logging directive example:

```bind
logging {
    category default { default_syslog };
    category queries { default_syslog };
};
```

> NOTE Line numbers have been added to the listing to add readability.

**The server Statement** The server statement tells BIND specific information about other name servers it may be dealing with. The format of the server statement is follows:

```bind
server ip-address {
    bogus yes/no;
    keys { string; [string; ...] };
    transfer-format one-answer/many-answers;
    <other options>...
};
```

Here, ip-address in line 1 is the IPv4 or IPv6 address of the remote server in question. The Bogus option in line 2 is useful if you are dealing with another site that may be sending you information about a misconfiguration. The keys clause in line 3 specifies a key_id defined by the key statement, which can be used to secure transactions talking to the remote server. This key is used in generating a request signature that is appended to messages exchanged with the remote name server. In line 4, transfer-format, tells BIND whether the remote name server can accept multiple answers in a single query response.
