output device. The overall effect of this is to print a list of all the pathnames that find discovers with the file name passwd on the end.

In this way you can find a list of pathnames without piping to grep as in previous examples. There is a difference, however: the -name expression will only look for complete words on the end of a pathname, whereas grep can look for substrings:

```
$ cd
$ find . -name motd -print 2>/dev/null
./text/motd
$ find . -print 2>/dev/null | grep motd
./text/motd
./backup/motd.bak
```

As a final, and more complex, example, let us see how we might generate a list of pathnames of all the ordinary files in a directory subtree whose contents include a particular string. One possible solution is to use find to generate the pathnames and then to use grep to see if the specified string appears in any of the files, printing the pathname of any files for which this is true. The only real problem is that grep normally displays any lines that it finds to the standard output as well as sending any error messages to the standard error device. One way round this problem is to redirect both the standard output and error output to /dev/null, but, in fact, grep provides an easier solution than this because it has command line switches built in to suppress these outputs for you:

```
$ find /etc -type f -exec grep -q -s mycroft {} \; -print
/etc/HOSTNAME
/etc/hosts
/etc/lilo.conf
```

What this command line does is to use find to generate a list of all the pathnames under the directory /etc. It then evaluates the expression -type f which returns the value true if the current pathname is an ordinary file. The second expression (-exec grep -q -s mycroft {} \; ) is thus evaluated for all the ordinary files, and searches each of them in turn for the string mycroft. Don't forget that the notation {} is replaced by the current pathname when grep is executed. The -q and -s options stop grep from producing its normal display, so that, effectively, this expression is just being used to generate a true or false value which decides whether or not to evaluate the third expression. The \ before the semi-colon at the end of the second expression is just to quote the semi-colon so the shell will ignore it and pass it to find unchanged. If the -exec grep expression returns true, then the -print expression will be evaluated which, as its action, will display the current pathname, as required.