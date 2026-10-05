# Listing 4.1 Contents of the cf/cf Subdirectory

```
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
graphic-hpux10.mc
graphic-hpux9.mc
graphic-linux.mc
graphic-linux.mc
graphic-nextstep3.3.mc
graphic-osf1.mc
graphic-osf1.mc
generic-solaris2.cf
generic-solaris2.mc
generic-sunos4.1.mc
generic-sunos4.1.mc
generic-ultrix4.cf
generic-ultrix4.mc
huginn.cs
knecht.mc
mail.cs.mc
mail.eecs.mc
mailpool.cs
python.cs.mc
s2k-osf1.mc
s2k-ultrix4.mc
tctproto.mc
test.cf
test.mc
uucbarpa.mc
uucbax.mc
uucppro.mc
vangogh.cs.mc
```
```

Most of these files—more than 30 of them—are sample macro control files. You can identify a control file by the .mc extension. Some are examples meant as educational tools. Others are prototypes or generic files meant to be the basis of your own configuration. Particularly interesting are the generic files for use with different operating systems. Generic files for Solaris, HPUX, BSD, Linux, and several other operating systems are included. For a Linux system administrator, the generic-linux.mc file is the one that gathers the most attention.

Several of the are identified by the .cf extension. These files are the result of processing macro configuration files through .mc and are already in the proper format to be used as the sendmail.cf file. It is unlikely, however, that you will use one of these files directly. Unless the generic macro configuration file is exactly to your liking, the Sendmail configuration file produced from .mc file will not be what you want. For example, the problem we want to solve is that the /etc/sendmail.cf file on our sample system is not compatible with Sendmail 8.11. Using the generic-linux.cf file as the