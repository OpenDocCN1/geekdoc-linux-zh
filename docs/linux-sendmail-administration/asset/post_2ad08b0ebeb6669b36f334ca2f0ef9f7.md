
is never used, and thus the hack directory is almost never used. An ls -l of the hack directory shows that it contains just one file.

```
[craig]$ ls hack
ssubdomain.m4
```

The one file contained in the hack directory is an old fix that was used for a few months at Berkeley to handle a domain transition. The file is there only as an example. It could not be used by anyone but Berkeley and it is no longer of use to them. The domain name transition handled by this hack could now be handled more easily with the database features built into the current Sendmail. The hack directory and HACK command are still there, but there is simply no good reason to use them.

The cf/siteconfig directory contains files that define the UUCP connectivity for the mail server. The file lists the locally connected UUCP sites using a specific sendmail m4 syntax. The siteconfig directory contains four samples.

```
[craig]$ ls siteconfig
uucp.cogsci.m4 uucp.old.arpa.m4 uucp.ucbarpa.m4 uucp.ucbvax.m4
```

The siteconfig directory and the SITECONFIG command are still maintained for backward compatibility. However, this directory is obsolete and should no longer be used to define the UUCP connectivity for a UUCP mail server. Use the Sendmail databases described in Chapter 6, “Using Sendmail Databases,” if you need to define UUCP connectivity.

The last-used directory does not even map to an m4 macro command. It is the sh directory and it contains only one file.

```
[craig]$ ls -1 sh
total 2
-rw-r--r-- 1 craig  1128 Feb 7 1999 makeinfo.sh
```

Even the name of this file is different. All of the files we have seen so far are m4 macro source files. As they end with the .m4 extension. This file, however, ends with the .sh extension, indicating that it is a shell script. The permission bits show this, even though it is a shell script, it is not executable. It is probably not being used. Still, I'm curious. So I changed the permissions and ran the script.

```
[root]# chmod 744 makeinfo.sh
[root]# ./makeinfo.sh
```

## The cf Directory Structure

##### built by root@ibis.foobirds.org on Aug 17 09:36:03 EDT 2000

##### in /usr/local/src/sendmail-8.11.0/cf/sh

##### using as configuration include directory

define(`__HOST__`, ibis.foobirds.org)dnl

The script produces three lines of comments that could be used to identify who built the sendmail.cf file, when they built it, and in what directory. The third line includes the name of the configuration directory when this is actually run by m4. The last line of output assigns a value to a variable. Of course, you don't run this script. As I said, I was just curious. The script is used by the m4 process when it builds the sendmail.cf file. You never use this script directly, and you never use this directory to store any of your own configuration files.

## The domain Directory

The cf/domain directory is one of directories where you are most likely to store your own configuration files. The purpose of the domain directory is to hold m4 files that define configuration values that are specific to your domain or network. The configuration file you create for your environment is then used in the macro configuration file via the DOMAIN command. Because the intent is for you to create your own file, the six files shown when you use the domain directory are all examples.

```
craig$ ls domain
Berkeley.EDU.m4 EECS.Berkeley.EDU.m4 berkeley-only.m4
CS.Berkeley.EDU.m4 S2K.Berkeley.EDU.m4 generic.m4
```

When you create your own domain configuration file, start by copying the sample file generic.m4 to a name that is meaningful for your domain or network. For example, if your domain is foobirds.org you copy generic.m4 to foobirds.m4. Then edit the new file to set the values needed for your environment.

Creating your own domain file is an advanced configuration topic covered in later chapters. Basic configurations do not require a custom domain file.

## The cf/cf Subdirectory

Most of the work creating a basic configuration takes place in the cf/cf directory. This is the working directory of Sendmail configuration. It contains all of the configuration files, and it is where you will put your own m4 configuration file when you build a custom configuration. Listing 4.1 shows that the cf/cf directory contains more than 40 files.

![](img/b8082498451dba2bf0cf2907c85c4c83_105_0.png)

## Listing 4.1 Contents of the cf/cf Subdirectory

```
[craig]$ cd /usr/local/src/sendmail-8.11.0/cf
[craig]$ ls cf
Build
Makefile
chez.cs.mc
clientproto.mc
-hpus10.mc
-hpus9.mc
-osf1.mc
-solaris2.mc
-sunos4.1.mc
-ultrix4.mc
cyproproto.mc
graphic-bsd4.cf
graphic-hpux10.mc
generic-linux.mc
generic-nextstep.mc
generic-osf1.mc
generic-solaris2.mc
generic-sunos4.1.mc
generic-ultrix4.mc
mail.mc
s2k-osf1.mc
```

The script produces three lines of comments that could be used to identify who built the sendmail.cf file, when they built it, and in what directory. The third line includes the name of the configuration directory when this is actually run by m4. The last line of output assigns a value to a variable. Of course, you don't run this script. As I said, I was just curious. The script is used by the m4 process when it builds the sendmail.cf file. You never use this script directly, and you never use this directory to store any of your own configuration files.

The cf/domain directory is one of directories where you are most likely to store your own configuration files. The purpose of the domain directory is to hold m4 files that define configuration values that are specific to your domain or network. The configuration file you create for your environment is then used in the macro configuration file via the DOMAIN command. Because the intent is for you to create your own file, the six files shown when you use the domain directory are all examples.

When you create your own domain configuration file, start by copying the sample file generic.m4 to a name that is meaningful for your domain or network. For example, if your domain is foobirds.org you copy generic.m4 to foobirds.m4. Then edit the new file to set the values needed for your environment.

Creating your own domain file is an advanced configuration topic covered in later chapters. Basic configurations do not require a custom domain file.

Most of the work creating a basic configuration takes place in the cf/cf directory. This is the working directory of Sendmail configuration. It contains all of the configuration files, and it is where you will put your own m4 configuration file when you build a custom configuration. Listing 4.1 shows that the cf/cf directory contains more than 40 files.

The siteconfig directory and the SITECONFIG command are still maintained for backward compatibility. However, this directory is obsolete and should no longer be used to define the UUCP connectivity for a UUCP mail server. Use the Sendmail databases described in Chapter 6, “Using Sendmail Databases,” if you need to define UUCP connectivity.

The last-used directory does not even map to an m4 macro command. It is the sh directory and it contains only one file.

Even the name of this file is different. All of the files we have seen so far are m4 macro source files. As they end with the .m4 extension. This file, however, ends with the .sh extension, indicating that it is a shell script. The permission bits show this, even though it is a shell script, it is not executable. It is probably not being used. Still, I'm curious. So I changed the permissions and ran the script.

## 4.2 Testing the generic-linux.cf

The --.. illustrates the the the test the themail..cf.

```
[root]# sendmail -v t -C /sendmail.cf
Warning: .cf file is out of date: sendmail 8.11 supports version 9,  .cf file is version 8
No recipient addresses found in header
^D
[root]# sendmail -v t -C ./generic-linux.cf
./generic-linux.cf: line 66: file: cannot open
  '/etc/mail/local-names'
  : no file or directory
```

The first sendmail illustrates the problem with the old sendmail.cf file. It is version 8, and Sendmail 8.11 wants a 9 configuration file. The second test uses the -cf command-line argument to specify the generic-linux.cf as the Sendmail configuration file. It also fails. This time, the configuration is looking for a file named /etc/mail/local-names, which does not exist. We can fix the problem by creating the desired file or by simplifying the configuration so it doesn't need that file. In this case we use the latter approach. (We don't cover the local-host-names file until the next chapter.)

```4.3
[root]# #Build test.cf
Using M4=/usr/bin/m4
rm -f test.cf
/usr/bin/m4 .../cf.m4 test.cf > test.cf ||
  ( rm -f test.cf && exit 1)
chmod 444 test.cf
```

The Build script is easy to use. Provide the name of the output file you want to create an argument on the Build command line. The script replaces the .cf extension of the out-file with the extension .mc and uses the macro configuration file with name to
