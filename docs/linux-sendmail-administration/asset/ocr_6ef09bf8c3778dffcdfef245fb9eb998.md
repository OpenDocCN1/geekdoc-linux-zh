sendmail.cf file illustrates this problem, but as the test in Listing 4.2 shows, it doesn't
work for our sample system.

# 4.2 Testing the generic-linux.cf File

```
[root]# sendmail -v t -C /etc/sendmail.cf
Warning: .cf file is out of date: sendmail 8.11.0 supports version 9,
  .cf file is version 8
No recipient addresses found in header
^D
[root]# sendmail -v t -C ./generic-linux.cf
./generic-linux.cf: line 66: fileclass: cannot open
  '/etc/mail/local-host-names'
  : no file or directory
```

The first sendmail illustrates the problem we have with the old sendmail.cf file. It
is version 8, and Sendmail 8.11 wants a 9 configuration file. The second test uses
the -cf command-line argument to specify the generic-linux.cf file as the Sendmail
configuration file. It also fails. This time, the configuration is looking for a file
named /etc/mail/local-host-names, which does not exist. We can fix the problem by
creating the desired file or by simplifying the configuration so that it doesn't need that file.
In this case we use the latter approach. (We don't cover the local-host-names file
until the next chapter.)

# The cf/cf Build Script

New Sendmail configurations are generally built inside the cf/cf directory. Two of the
files in this directory are there to aid the build process. These are the Build script and
t Makefile it uses. Listing 4.3 shows a Sendmail configuration file being constructed
with the Build script.

# 4.3 Using the cf/cf/Build script

```
[root]# #Build test.cf
Using M4=/usr/bin/m4
rm -f test.cf
/usr/bin/m4 .../cf.m4 test.cf > test.cf ||
  ( rm -f test.cf && exit 1)
chmod 444 test.cf
```

The Build script is easy to use. Provide the name of the output file you want to create
an argument on the Build command line. The script replaces the .cf extension of the out-
file with the extension .mc and uses the macro configuration file with name to

![](bbox=[0.915, 0.298, 0.986, 0.38])