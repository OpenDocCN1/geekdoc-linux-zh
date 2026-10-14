
2009 is not a leap year
$ ./test17.py 2008
2008 is a leap year
$

As you can see from this example, Python is a little more complicated than Perl when using command-line arguments. The command-line argument is placed in the sys.argv array as element 1 (not 0 as in Perl). You might also notice that unlike Perl, Python is very specific about data types. The command-line arguments are all converted as string values.

Because the program needs to use the command-line argument as an integer value, it must be converted. The string module provides the atoi function, which converts ASCII strings to integer values. After assigning the new integer value to a variable, the calculations can begin.

However, in Python, special mathematical operators (such as the Boolean XOR) are also functions, and must be used as functions instead of operators. This requires importing the operators module and rewriting the if statements to use the xor() function.

## Python Modules

All object-oriented programming languages include libraries that contain pre-built classes that are useful to programmers. The Python programming language is no different.

In Python, class libraries are called *modules*. A module contains classes and functions that can be called from within a Python script. The standard Python installation includes a library of standard modules that are built into the interpreter. To reference classes and functions from the module, you must define the module name within the script using the import command, as was demonstrated in the previous section.

Here is an example of using the SMTP module to easily send a mail message from your Python script:

```
$ cat test18.py
#!/usr/bin/python
# using the SMTP module to send mail
import smtplib, time

From = "rich"
To = "rich"
Subject = "Test mail from Python"
Date = time.ctime(time.time())
Header = 'From: %s\nTo: %s\nDate: %s\nSubject: %s\n' % (From, To, Date, Subject)
Text = "This is a test message from my Python script"
server = smtplib.SMTP('localhost')
result = server.sendmail(From, To, Header + Text)
server.quit()
if result:
    print "problem sending message"
else:
    print "message successfully sent"
$ ./test18.py
```

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

## Summary

This chapter dove into the worlds of Perl and Python. The Perl scripting language has become a popular platform for system utilities, mostly because of its data-handling capabilities. Perl provides a simple way to scan data using regular expressions and easily manipulate the data however you need. The Ubuntu installation of Perl also uses the CPAN module, which allows Perl to connect with remote CPAN databases to update modules and load new modules to provide specific functionality to your system.

The Python scripting language provides an object-oriented programming approach to scripted languages. It references items as objects, and provides lots of methods to easily manipulate objects within the script. Similar to Perl, Python also uses modules to provide additional functionality to the core features.

The next chapter looks at a higher-level programming platform available in Ubuntu, the C programming language. The Linux platform has been built around the C programming language, and many Open Source programs and utilities require a C programming environment to install properly. We’ll take a look at the C programming environment provided by Ubuntu, and see how to use the C programming language to build our own projects.
