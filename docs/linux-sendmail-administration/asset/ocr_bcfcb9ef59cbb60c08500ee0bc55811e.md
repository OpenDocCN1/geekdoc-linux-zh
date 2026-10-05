# Installing Sendmail

It is the worst-case scenario. We had hoped everything would be easy sailing. Now we need to track all the packages needed by Sendmail 8.11, install those packages, and then attempt to install sendmail-8.11.0-1.i386.rpm all over again. This bit of unpleasantness is a blessing in disguise. If we installed sendmail-8.11.0-1.i386.rpm from source and did not know that openssl and libssl are required, the features of Sendmail would not work as advertised. It could take a long time tracking down the problem. RPM makes sure that we know the problem right from the start. We could force RPM to install sendmail-8.11.0-1.i386.rpm without the dependencies by adding the --nodeps argument to rpm command. But the best thing to do is track down and install the required packages.

A search of rpmfind informs us that we need three different RPM packages to fix the six dependencies: openssl-0.9.sa-1.i386.rpm, lib5io-1999-1.i386.rpm, and cyrus-sas1-1.5.11-2.i386.rpm. The first two packages, openssl and libssl, are pretty obvious RPM lists them as the first two dependencies needed by sendmail-8.11.0-1.i386.rpm. An examination of the list of files provided by each package shows that they provide every dependency except libsas1.so. A search for libsas1-so.7 tells us that it is found in cyrus-sas1-1.5.11-2.i386.rpm. We download the three packages and install them as shown in Listing 3.8.

# Listing 3.8 Fixing Dependency Problems for Sendmail 8.11

```
[root]# - rpm openssl-0.9.sa-1.i386.rpm
error: file /usr/man/man/passwd from install of openssl-0.9.sa-1
conflicts with file from package passwd-0.58-1
[root]# - rpm --replacefiles openssl-0.9.sa-1.i386.rpm
[root]# - rpm lib5io-1999-1.i386.rpm
[root]# - rpm -u sendmail-8.11.0-1.i386.rpm
[root]# - rpm q sendmail
sendmail-8.11.0-1
```

Even this installation did not go perfectly. The openssl-0.9.sa-1.i386.rpm package creates a new passwd page. The problem is, it doesn't own the old page. That page was on the system by the passwd-0.58-1.i386.rpm package. RPM wont let a new package change a file that belongs to another unless you tell it to. In this case, we want the new passwd documentation so we use the --replacefiles argument with the rpm command to replace the old passwd documentation with the new documentation.