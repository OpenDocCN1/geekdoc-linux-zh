# 432 Linux Administration: A Beginner's Guide

+   - /usr/bin/host A program performs a simple query on a name server.
- /usr/bin/dig A program that performs complex queries on a name server. The remainder of the chapter will discuss some of the programs/utilities listed here, as well as their configuration and usage.

# Understanding the BIND Configuration File

The named.conf file is the main configuration file for BIND. Based on this file's specifications, BIND determines how it should behave and what additional configuration files, if any, must be read. This section covers what you need to set up a general-purpose DNS server. You'll find a complete guide to the new configuration file format in the html of BIND's documentation.

The general format of the named.conf file is as follows:

```
statement {
options; // comments
}
```

The statement keyword tells BIND we're about to describe a particular facet of its operation, and options are the commands applying to that statement. The curly braces are required so that BIND knows which options are related to which statements; a semicolon follows every option and after the closing curly brace.
 example of this follows:

```
options {
directory "/var/named"; // put config files in /var/named
}
```

This Bind means that this is an option statement. The particular option here is the directive that specifies BIND's working directory—that is, the directory on the local system that will hold the name server's configuration data.

# The Specifics

This section documents the many comments you will see in a typical named.conf file. The best way to tackle this is to skim it first, and then treat it as a reference guide for later sections. If some of the directives seem bizarre or don't make sense during your first pass, don't worry. Once you see them in use later sections, the hows and whys will quickly fall into place.

# Comments

Comments can be in one of the following formats:

| Format | Indicates |
|---||
| // | C++-style comments |
| /*...*/ | C-style comments |
| # | Perl and UNIX shell script-style comments |