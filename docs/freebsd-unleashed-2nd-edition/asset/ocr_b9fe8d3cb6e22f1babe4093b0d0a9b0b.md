It's possible for Perl to fail to open the file, either because it doesn't exist, its permissions don't allow you to read it, or any other of a number of reasons. You can trap for failures opening the file by using the **die** operator; if the evaluation of an expression falls through to **die**, it will print its argument (if any) to standard output, and the script will quit. Here's the most common way **die** is used with opening files:

```
open (FH,"/path/to/file1.txt") || die ("Can't open file1.txt!");
@contents = <FH>;
close (FH);
```

Writing to files is a bit more complex because there are so many different ways you can do it. The thing to remember is that you can write to any kind of handle you can use on the command line, which includes the overwrite (>) or append (>>) redirector, or even the \| (pipe) into a program. This is useful for, say, having your script write its output into an e-mail message:

```
open (FH,">/path/to/file2.txt");
print FH $_ foreach (@contents);
close (FH);
```

```
open (MAIL,"| /sbin/sendmail -oi -t");
print MAIL "From: me@somewhere.com\n";
print MAIL "To: you@somewhereelse.com\n";
print MAIL "Subject: Check it out!\n\n";
print MAIL $_ foreach (@contents);
close (MAIL);
```

> **CAUTION**
> Remember that when specifying @ characters in text strings (in e-mail addresses, for instance), you need to precede them with backslashes to prevent Perl from treating them as array identifiers. If you don't, the script will fail with an error.

The filehandle goes as an argument to **print**; it's important here to realize that this argument is assumed to be the built-in filehandle <STDOUT> (standard output), unless a different one is specified. There is also a <STDIN> handle. To set the default input/output filehandle, use the **select()** function:

```
select (FH);
```

This way, you won't have to write **print FH** every time. However, you'll need to switch it back to **STDOUT** when you're done with **FH**.