# LISTING 18.14 continued

```
afpovertcp 548/tcp      # AFP over TCP
afpovertcp 548/udp      # AFP over TCP
```

If you issue the commands as shown and do not get these six entries back, you must add them to /etc/services yourself. To do this, you can append the file /usr/doc/netatalk-1.4b2+asun2.1.3/services.atalk onto the end of your /etc/services file, or you can edit the file by hand and add the entries as shown above.

# netatalk Configuration Files

With /etc/services set up properly, you can start work on the netatalk configuration files. The first of these is the atalkd.conf file, which the netatalk rpm installs in /etc/atalk. The file that is installed by the netatalk package is for all intents and purposes empty, since it contains only comments. This should be sufficient for most installs; however, if it is not, you can refer to the installed file for instructions on what to put there. This configuration file is utilized by the atalkd, which is the class AppleTalk kernel interface. This daemon serves as the link between the classic AppleTalk functions of the netatalk package and the AppleTalk module that you loaded into the kernel.

# afpd.conf File

The next file we are concerned with is the afpd.conf file, which is used to set classic AppleTalk and AppleShare IP server options. In its simplest form, this file is also empty, just like the atalkd.conf file. However, this file has many more options than the atalkd.conf file and if you require a more complicated setup than the default, you can refer to the afpd manual page and the comments in the installed file to guide you in setting this up.

Sounds easy so far. The final files that we will be working with prior to attempting to turn on AppleTalk services are the AppleVolumes.default and the AppleVolumes.system files. These files define the services that are advertised to AppleTalk clients on the network. The first of these is the AppleVolumes.system file. This file is similar in function to the .mailcap file found in user home directories in that it provides information on file type to application associations. The format of the file is quite simple and includes an extension, a file type, the program associated with creating the file, and the program to run when the file is double clicked. Listing 18.15 is the AppleVolumes.system file that is included in the netatalk package. As you will see, it contains quite a few entries.