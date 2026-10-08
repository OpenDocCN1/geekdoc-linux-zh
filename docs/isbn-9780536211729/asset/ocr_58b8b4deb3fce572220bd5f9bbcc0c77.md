+   - check_wtmpx
- chkproc
- chkdirs
- strings

Of all the tools used in this book, Chkrootkit is probably the easiest to use. To run Chkrootkit, from within the `chkrootkit` source directory you simply type this:

```
./chkrootkit | less
```

You aren’t required to pipe the output to less but there is a copious amount of output. So if you actually want to read the output, you’ll probably need to pipe it somewhere—unless, of course, you have a huge scrollback buffer.

Because running Chkrootkit produces a lot of output, it is wise to pipe the output to more or less, depending on your preference. Alternatively, you could redirect the output to a file:

```
./chkrootkit > output.txt
```

Chkrootkit will output a number of lines informing you what it is currently checking for along with the ultimate status of the check. The output will look similar to this:

```
Checking `amd`... not found
Checking `basename`... not infected
Checking `biff`... not infected
Checking `chfn`... not infected
Checking `chsh`... not infected
Searching for ShitC Worm... nothing found
Searching for Ome ga Worm... nothing found
Searching for Sadmin/IIIS Worm... nothing found
Searching for MonKit... nothing found
Searching for Showtee... nothing found
```

As you can see from the output sample, it doesn’t appear that any trojaned files or rootkits were detected. An infected file or detection of a rootkit will look similar to the following:

```
Checking `bindshell`... INFECTED (PORTS: 1524 31337)
```

Even though the output from Chkrootkit seems to indicate that the computer is infected with bindshell, Chkrootkit does sometimes produce false positives. However, if you see the INFECTED output from Chkrootkit, it’s in your best interest to assume that Chkrootkit reported correctly and take steps to mitigate the damage.

A false positive occurs when a tool detects and reports a problem when in fact there is no problem. The underlying cause for false positives varies depending on the nature of the software reporting the occurrence. False positives are not as bad as false negatives. A false negative occurs when there really is a problem but the problem is not reported by tools that should find the problem.