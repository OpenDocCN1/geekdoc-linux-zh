After the program is built and installed, you might have to do additional configuration. You should consult the *man* pages or the HOWTOs that come with the software for information on how to proceed.

> **TIP:** With some *tar.gz* files that include an RPM spec file, you could run the *rpm -ta file.tar.gz* and the *rpm* command will build an RPM from that tarball.

To try out this procedure, I downloaded the whichman package, which includes utilities that let you find manual pages by entering keywords. The file I downloaded, whichman-2.2.tar.gz, was placed in a directory that I created called */usr/src/which*. I then ran the *gunzip* and *tar* commands, using *whichman-2.2.tar.gz* and *whichman-2.2.tar* as arguments, respectively.

I changed to the new directory, *cd /usr/sw/which/whichman-2.2*. I then listed its contents. The README file contained information about the contents of the package and how to install it. As the README file suggested, I typed *make*, and then *make install*. The commands *whichman*, *fwhich*, and *ftff* were installed in */usr/bin*. (At this point, you can check the *man* page for each component to see what it does.)

The last thing I found in the README file was that a bit of configuration needed to be done. I added a MANPATH variable to my *$HOME/.bashrc* to identify the location of *man* pages on my computer to be searched by the *whichman* utility. The line I added looked like this:

```
export MANPATH=/usr/share/man:/usr/man/man1:/usr/X11R6/man:/usr/share/doc/samba-2.2.3a/docs
```

In case you are wondering, *whichman*, *fwhich*, and *ff* are commands that you can use to search for *man* pages. They can be used to find several locations of a *man* page, *man* pages that are close to the name you enter, or *man* pages that are located beneath a point in the directory structure, respectively.

# Using Fedora or RHEL to Run Applications

Although operating systems are nice (and necessary), people use desktop computers to run application programs. There has been a common belief that although Fedora or RHEL can work well as a server, they are not ready to challenge Microsoft’s dominance of the desktop arena. There are several reasons why, I believe, Fedora and RHEL can replace Microsoft Windows on the desktop, if you are committed to doing it:

+   * Every category of desktop application now has an open source offering that will run in Linux. So, for *example*, although Adobe Photoshop doesn’t run natively in Linux, you can use the GIMP or other applications to work with digital images in Linux.
+   * Your Windows applications that you absolutely must have can usually be run without problems using Windows emulators or compatibility programs, such as QEMU and