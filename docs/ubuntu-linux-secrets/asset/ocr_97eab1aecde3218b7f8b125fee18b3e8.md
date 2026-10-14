```
message successfully sent
$ mail
Mail version 8.1.2 01/15/2001. Type ? for help.
"*/var/mail/rich": 1 message 1 new
>N 1 rich@testbox.local Fri Nov 7 06:56 15/553 Test mail from Python
&
Message 1:
From: rich@testbox.localdomain Fri Nov 7 06:56:44 2008
X-Original-To: rich
From: rich@testbox.localdomain
To: rich@testbox.localdomain
Date: Fri Nov 7 06:56:43 2008
Subject: Test mail from Python

This is a test message from my Python script

&
```

This sample program imports two standard modules. The smtp lib module provides SMTP functions, and the time module provides modules for getting the time from the system.

The script uses the SMTP Python module, which interfaces with the mail program on the local system to send the created message. If you do not have your mail system configured, this script won’t work.

Besides the standard modules, there are a host of other modules available for just about any type of programming function. Scanning the Web for the term "Python modules" produces thousands of code modules freely available to incorporate into your own applications.

# Summary

This chapter dove into the worlds of Perl and Python. The Perl scripting language has become a popular platform for system utilities, mostly because of its data-handling capabilities. Perl provides a simple way to scan data using regular expressions and easily manipulate the data however you need. The Ubuntu installation of Perl also uses the CPAN module, which allows Perl to connect with remote CPAN databases to update modules and load new modules to provide specific functionality to your system.

The Python scripting language provides an object-oriented programming approach to scripted languages. It references items as objects, and provides lots of methods to easily manipulate objects within the script. Similar to Perl, Python also uses modules to provide additional functionality to the core features.

The next chapter looks at a higher-level programming platform available in Ubuntu, the C programming language. The Linux platform has been built around the C programming language, and many Open Source programs and utilities require a C programming environment to install properly. We’ll take a look at the C programming environment provided by Ubuntu, and see how to use the C programming language to build our own projects.