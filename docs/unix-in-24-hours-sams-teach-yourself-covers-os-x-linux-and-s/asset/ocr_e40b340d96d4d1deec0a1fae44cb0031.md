# Hour 2. Getting onto the System and Using the Command Line

# Goals for This Hour

In this hour, you will learn

+   - How to log in to and log out of the system
+   - How to change your password with the `passwd` command
+   - About choosing a memorable and secure password
+   - How to find out who the computer thinks you are
+   - How to find out who else is on the system
+   - How to find out what everyone is doing on the system
+   - About checking the current date and time

In this second Unix lesson, it’s time for you to log in to the system and try some commands. This hour focuses on learning the basics of interacting with your Unix machine.

This hour introduces many commands, so it’s very important that you have a Unix system available on which you can work through all the examples. Most examples have been taken from a PC running Solaris 11, a variant of Unix System V Release 4, and have been double-checked on both a BSD-based system and a Mac OS X command line. Any variance between the three is noted. If you have a Unix system available, odds are good that it’s based on either AT&T System V or Berkeley Unix.

# Beginning Your Session

Before you can start interacting with the Unix command shell of your choice, you need to learn how to log in to your account. The good news is that it’s easy! Let’s have a look.

# Task 2.1: Logging In to and Out of the System

Because Unix is a multiuser system, user authentication is always enforced: You always need to provide credentials (generally a username and a password) to the system so that it knows who you are. Some modern user-friendly flavors of Unix (such as Mac OS X) allow you to bypass this requirement by always booting into a single user’s desktop session, but this is just a convenience feature; under the hood, all Unix flavors are the same, and all require that you authenticate yourself at some stage of the process.