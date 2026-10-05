# Python quick start

making major investments in Python scriptability. Ruby, by contrast, is primarily associated with web development and is rarely used for general scripting.

Python was created by Guido van Rosum. It's easier to code and more readable than Perl. Python offers a simple-to-understand syntax that is easy to follow even if you didn't develop the code. If you're tired of remembering which comparison operators to, you'll appreciate Python's unified approach. Python also offers additional data types that system administrators find useful.

If Python is not already on your system, check your vendor's or distributor's list of available packages. It is an extremely common package and should be universally available. Failing that, you can get Python source code from python.org. That is also a central location for finding-in modules developed by others.

For a more thorough introduction to Python than we can give here, Mark Pilgrim's Dive Into Python is a great place to start. It's available for reading or for download (without charge) at divintopython.org, or as a printed book from Apress. A complete citation can be found on page 75.

# Python quick start

As usual with a quick "Hello, world!" script. As it happens, Python's "Hello, world!" is almost identical to Perl's.

```
#!/usr/bin/python
print "Hello, world!"
```

To get it running, set the execute bit or invoke the python interpreter directly:

```
$ chmod +x heloworld
./helloworld
Hello, world!
```

This one-liner fails to illustrate Python's most scandalous break with tradition, namely that indentation is logically significant. Python does not use braces, brackets, or begin and end to delineate blocks. Statements at the same level of indentation automatically form blocks. The exact indentation style (spaces or tabs, depth of indentation) does not matter. Python blocking is best shown by example, here is an if-then-else statement:

```
#!/usr/bin/python
import sys
a = sys.argv[1]

if a == "1":
    print 'a is one'
    print 'This is still the clause of the if statement.'
else:
    print 'a is is', a
    print 'This is still the else clause of the if statement.'
```

print 'This is after the if statement.'

![](bbox=[0.958, 0.137, 0.992, 0.245])