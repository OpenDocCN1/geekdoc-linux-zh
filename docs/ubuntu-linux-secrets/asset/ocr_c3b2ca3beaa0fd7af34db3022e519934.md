2009 is not a leap year
$ ./test17.py 2008
2008 is a leap year
$

As you can see from this example, Python is a little more complicated than Perl when using command-line arguments. The command-line argument is placed in the sys.argv array as element 1 (not 0 as in Perl). You might also notice that unlike Perl, Python is very specific about data types. The command-line arguments are all converted as string values.

Because the program needs to use the command-line argument as an integer value, it must be converted. The string module provides the atoi function, which converts ASCII strings to integer values. After assigning the new integer value to a variable, the calculations can begin.

However, in Python, special mathematical operators (such as the Boolean XOR) are also functions, and must be used as functions instead of operators. This requires importing the operators module and rewriting the if statements to use the xor() function.

# Python Modules

All object-oriented programming languages include libraries that contain pre-built classes that are useful to programmers. The Python programming language is no different.

In Python, class libraries are called *modules*. A module contains classes and functions that can be called from within a Python script. The standard Python installation includes a library of standard modules that are built into the interpreter. To reference classes and functions from the module, you must define the module name within the script using the import command, as was demonstrated in the previous section.

Here is an example of using the SMTP module to easily send a mail message from your Python script:

```
```python
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