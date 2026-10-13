When this program chooses the word "umbrella," the encrypted password will be same as the one stored in /etc/passwd. Too bad, bob's password has just been cracked! Now the program knows which word (umbrella) was used to create the password. This is the simplified explanation of how cracking software works. However, bear in mind that today's cracking software is much more advanced, and as computer hardware becomes more and more powerful, cracking passwords becomes easier and faster.

# Installing Crack to crack your own passwords

To crack your system's passwords, you need a password-cracking program. Crack is one such widely used, free software package. You can download an RPM package version of Crack from many of the Red Hat mirror sites that keep user-contributed software. One such site is http://ftp.digital.com/pub/linux/redhat/contrib/.

You have to go into the directory corresponding to your system's architecture, such as i386 (x86 or Intel), sparc (Sun Microsystems), alpha (Digital Alpha), and so on, and download the crack-X.xx-x.(architecture).rpm, where X.xx-x is a version number and (architecture) is your system's architecture. For example, for an x86 or Intel-based system, download crack-4.1f-1.1386.rpm. The version number may vary, because newer versions are uploaded over time.

After you upload the RPM package, install it as follows:

```
rpm -ivh crack_package_name.rpm
```

You then can find out what files got installed, by running the following command:

```
rpm -qi crack_package_name
```

Typically, Crack gets installed in /root/Crack-X.xx/ directory.

# Running Crack

To run the Crack program from the installed directory, use the following command:

```
Crack /etc/passwd
```