initially to set the CPAN module, which will allow you to automatically download and install Perl modules as you need them.

The manual method is similar to the methods used earlier to download and install both the OpenSSL and OpenSSH programs, and only minimal instructions are included here. After you have latest Net_SSLeay tarball, open it, cd into the directory, and run the following command (as root):

```
perl Makefile.PL; make; make test; make install
```

This will take care of building, testing, and installing the Perl module. The source tarball can be obtained from the following URL:

http://cpan.valueclick.com/authors/id/S/SA/SAMPO/Net-SSLeay.pm-1.05.tar.gz

To use the CPAN module, you’ll need to do some setup first, but this setup is all automated. You’ll only go through the setup steps the first time and, whenever you need a Perl module, you need only invoke the CPAN module and tell it to install the Perl module you need. At the root prompt, type the following:

```
perl -MCPAN -e shell
```

The first time you do this, you walk through the configuration. If in doubt, choose the defaults. You need to decide where you want CPAN to look to download the Perl modules, but you’ll be given an extensive (possibly too extensive) list. Choose three or so (nearby) sites and continue.

After everything is set up, CPAN downloads the latest list of modules. It does this every time you run it if the list is over 24 hours old. Finally, you will end up at a CPAN prompt:

```
cpan>
```

Just tell it the module you want to install:

```
install Net::SSLeay
```

CPAN downloads the tarball, checks its authenticity and integrity (CPAN will tell you whether you need to install other modules such as the MD5 bundle), and then runs the make, make test, and install.

If any Perl modules require other Perl modules, CPAN handles the dependency checking and installs those modules as well. The CPAN utility is friendly and tries to help you if it doesn’t understand what you want. Just follow the instructions it supplies.

# WEBMIN

One of the nicest and easiest local and remote administration tools to appear on the scene is Webmin. This particular utility has been around for several years, but Caldera has finally decided to adopt it for remote administration. This tool can also be used for local administration, and in its “out of the box” configuration, should be used only locally, because encryption is not included.