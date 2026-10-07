# Installing Sendmail with RPM

Once the package is located, it can be installed using the rpm command. The rpm command is similar to the Debian dpkg command. It allows you to check the status of installed packages, remove outdated packages, and install updates.

Use the rpm command with the -q option or the --query option to check what packages are already installed in the system.

```
[raig]$ rpm --query sendmail
sendmail-8.9.3-10
```

This example queries rpm for the string sendmail. The response shows that Sendmail version 8.9.3 is installed on our sample system. At the time of this writing, the latest RPM version of Sendmail available from www.rpmfind.net and www.redhat.com is, so we decide to upgrade the sample system.

Before installing a new version of an RPM package, you can remove the old one by running rpm with the --erase option. See the section "Cleaning Up After RPM" later in this chapter for an example of this). Removing the old Sendmail RPM package is probably a good idea if you plan to compile and install the Sendmail program from the source code distribution. But if you plan to install a new RPM version of Sendmail, removing the old package is unnecessary. Use the -U option with the rpm command, as shown in Listing 3.7, to update an existing RPM installation with a newer package.

# 3.7 Updating Sendmail with RPM

```
[root]# # rpm -U sendmail-doc-8.11.0-1.i386.rpm
[root]# # rpm -U sendmail-cf-8.11.0-1.i386.rpm
[root]# # rpm -U sendmail-8.11.0-1.i386.rpm
```

```
error: failed dependencies:
openssl is needed by sendmail-8.11.0-1
libsio is needed by sendmail-8.11.0-1
libcrypto.so is needed by sendmail-8.11.0-1
libsas1.so.7 is needed by sendmail-8.11.0-1
libsio is needed by sendmail-8.11.0-1
libs1.so.0 is needed by sendmail-8.11.0-1
```

The Sendmail 8.11 package is composed of three components: the documents, the configuration files, and Sendmail itself. In Listing 3.7 the configuration and file components install without a hitch. The third component, however, fails to install. RPM informs us that several pieces of software required by Sendmail 8.11 are not available on this sample system. RPM calls required software dependencies. Sometimes other software depends on the package you're installing or removing, and sometimes the software you're depends on other software.