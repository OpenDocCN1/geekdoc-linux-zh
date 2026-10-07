# CHAPTER 8 Managing Software and System Resources

This example also uses the v and h options, which provide a more verbose output
display of hash marks to show the progress of the installation. You can also use rpm to
query its database after installing packages to verify an installation.

Use the -V option, along with the name of a software package, to verify installation
system. For example, to verify the pine package, use the rpm command like this:

```
# rpm -V pine
```

> NOTE
Note if everything is correct with your software installation, your system will display no
response to rpm -V after you run the command; only problems are displayed.

As you can see from the following program output, you can get additional information
out a package by adding additional verification options (such as two more vs) to the -V
option. To get more information about an installed package, use one or more forms of the
rpm query options. For example, to display concise information about an installed
package, use the -q option, along with the i and the installed package name, like
(that note your version will differ from that shown here):

```
# rpm -qi pine
Name : pine Relocations: (not relocatable)
Version : 4.44 Vendor: Red Hat, Inc.
Release : 7 Build Date: Wed 17 \
Apr 2002 04:07:44 PM EDT
Install date: Fri 10 May 2002 11:35:27 AM EDT \
nBuild Host: stripples.devel.redhat.com
Group : Applications/Internet Source rpm: pine-4.44-7.src.rpm
Size : 6725592 License: Freely Distributable
Packager : Red Hat, Inc. http://bugzilla.redhat.com/bugzilla/
URL : http://www.washington.com/pine/
Summary : A common used, MIME compliant mail and readers user agent
Description :
Pine is a very popular, easy to use, full-featured email editor called Pine. Pine supports MIME
ensions and includes a simple text editor called and can also be used to read news. Pine also supports IMAP,
mail, and MH style folders.
```

This form of rpm query provides a bit of information about the software package.
(You can also query packages before installation by providing a pathname for them.)

If this package isn't up-to-date, you can easily and quickly upgrade the package by down-loading a newer version and then using rpm's -U or upgrade option like this: