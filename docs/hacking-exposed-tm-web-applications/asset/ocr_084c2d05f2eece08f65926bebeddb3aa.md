# Chapter 8: Input Validation Attacks

# 205

# COMMON INPUT VALIDATION ATTACKS

Let's take a look at some common payloads for an input validation attack. Even though many of the tests merely dump garbage characters into the application, there are other tests that require specifically formatted strings. For the most part, we'll just test for the presence of a vulnerability and leave actual exploitation to another chapter. For example, the fulcrum for SQL injection is input validation (especially applications that do not validate the query); however, a full discussion of SQL injection is covered in Chapter 9.

# Buffer Overflow

To execute a buffer overflow attack, you merely dump as much data as possible into an input field. This is the most brutal and ignorant of attacks, but useful when it returns an application error. Perl is well-suited for this task. One instruction will create whatever length necessary to launch the attack:

```
$ perl -e 'print "a" x 500\naaaaa...repeated 500 times
```

You can create a Perl script to make the HTTP requests, or dump the output through netcat. Instead of submitting the normal argument, wrap the Perl line in back ticks and replace the argument. Here is the normal request:

```
$ echo "GET /login.php?user=faustus\nHTTP/1.0\n\n" | \
c -vv www.victim.com 80
```

And here is the buffer test, calling on Perl from the command line:

```
$ echo "GET /login.php?user=\n> perl -e 'print "a" x 500\nHTTP/1.0\n\n" | \
c -vv www.victim.com 80
```

This sends a string of 500 a's for the "user" value to the login file. This Perl trick can be used anywhere on the UNIX (or Cygwin) command line. For example, combining this technique with the curl program reduces the problem of dealing with SSL:

```
$ curl https://www.victim.com/login.php?user=-perl -e 'print "a" x 500`
```

Another tool, NTOMax, provides more features to automate buffer overflow tests. NTOMax is simple to use. Its real strength lies in its support of scripts. Here is the basic usage:

```
C:\NTOMax.exe / ?
```

Seek and Destroy - Information Warfare
NTOMax v2.0 - Copyright(c) 1999, Foundation, Inc.
Server stress tester for buffer overflow/DOS conditions