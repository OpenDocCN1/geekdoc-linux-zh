technique, anyone can learn a great deal about your system. For example, replacing the `ps` command with `df` (a common Unix utility that prints a summary of disk space) enables anyone to determine what partitions you have and how full they are. This security hole could pose a great danger.

What is the lesson? It is not to trust any input, and not to make system calls an easy target for abuse. How to achieve these goals is the topic that is addressed in the next section.

# User can modify hidden data in HTML pages

As you might already know, HTTP is a stateless protocol. Many Web developers keep state information or other important data in cookies, or temporary files, or using so called hidden tags. Because a user can turn off cookies and because creating unique temporary files per user is cumbersome, hidden tags are commonly used. A hidden tag looks similar to the following:

```
`<input type="hidden" name="dataKey" value="dataValue">`
```

For example:

```
`<input type="hidden" name="state" value="CA">`
```

Here the hidden tag stores "state=CA," which can be retrieved by the same application in a subsequent call. Hidden tags are common in multiscreen Web applications. Because the user can manually change hidden tags, they should not be trusted. There are two ways of protecting against altered data: the developer can verify the hidden data before each use, or the developer can use a security scheme to ensure that data has not be altered by the user. The CGI script shown in Listing 18-2, demonstrates the use of the RSA Data Security MD5 message digest algorithm to protect hidden data.

![](bbox=[0.15, 0.65, 0.22, 0.7])

The details of the MD5 algorithm are defined in RFC 1321.

# Listing 18-2: hidden-md5,eg

```
#!/usr/bin/perl -w
#
# Purpose: This script demonstrates the use of
# MD5 message digest in a multistcreen
# Web application.
#
# CVS: $Id$
# #####################################################################################
use strict;
```