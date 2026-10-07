All of the other installations run smoothly. Once the dependencies are resolved, sendmail-8.11-0.1.i386.rpm installs without complaint. A quick query to RPM shows that the new package is installed

Next, restart Sendmail to make sure the newly installed daemon is running, and run a quick test to make sure the new daemon is alive and servicing the SMTP port. Listing 3.9 shows these two commands.

# Listing 3.9 Restarting and Testing Sendmail

```
[root]# /etc/rc.d/sendmail restart [ OK ]
Shutting down sendmail:
Starting sendmail: [ OK ]
[root]# telnet localhost 25
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'
220 wen.foobirds.org SMTP Sendmail 8.11.0/8.11.0;
Sun, 13 Aug 2000 18:00:03 -0400
quit
221 2.0.0 wen.foobirds.org closing connection
Connection closed by foreign host.
```

As Listing 3.9 shows, Sendmail 8.11 is installed and running. Despite all of the problems encountered in this installation, Sendmail is upgraded and running after fewer than a dozen commands. Linux package managers have done much to simplify upgrades.

> NOTE I have never had a problem with dependencies upgrading Sendmail before 8.11. This just turned out to be a lucky break. Normally, things go so smoothly when preparing examples for Linux books that problems have to be described without actual examples. This time we were lucky enough to have a real problem. You might need see dependency problems when installing Sendmail yourself, but it is good to know how they are resolved.

# X Tools for Installing Sendmail

In the previous section, we used the command-line version of rpm. It is easy, easy to explain, and it runs on many Linux systems—even those that don't have X Windows running. If you are using X Windows, there are some graphical tools for running the Red Hat Package Manager. Several systems use a tool named glint. Systems with the KDE desktop environment use a tool named kpackageage, and systems with the GNOME