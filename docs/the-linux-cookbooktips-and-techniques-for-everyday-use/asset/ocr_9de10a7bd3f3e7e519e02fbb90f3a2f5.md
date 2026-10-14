# The Linux Cookbook: Tips and Techniques for Everyday Use:

can use zless instead of less.

The Linux Documentation Project (LDP) has overseen the creation of more than 100 "HOWTO" files, each of which covers a particular aspect of the installation or use of Linux-based systems.

The LDP HOWTOs are compressed text files stored in the `/usr/doc/HOWTO` directory; to view them, use zless. The file `/usr/doc/HOWTO/HOWTO-Index.gz` contains an annotated index of all the HOWTO documents installed on the system.[1]

Finally, the `/usr/doc/FAQ` directory contains a number of FAQ ("Frequently Asked Questions") files on various subjects, and the files that make up the Debian FAQ are in the `/usr/doc/debian/FAQ` directory. The Debian FAQ is available both in HTML format, which you can view in a Web browser (see section Browsing Files), and as a compressed text file, which you can view in zless.

+   - To view the HTML version of the Debian FAQ in the lynx Web browser, type:

```
$ lynx /usr/doc/debian/FAQ/debian-faq.html RET
```

+   - To view the compressed text version of the Debian FAQ in zless, type:

```
$ zless /usr/doc/debian/FAQ/debian-faq.txt.gz RET
```

NOTE: It's often very useful to use a Web browser to browse through the documentation files in these directories—see Browsing Files.

On some systems, `/usr/doc` is superseded by the `/usr/share/doc` directory.