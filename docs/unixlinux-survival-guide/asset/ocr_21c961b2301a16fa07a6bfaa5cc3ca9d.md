To convert the number 7 to binary, for example, you use the commands shown in Listing 6.18.

# LISTING 6.18 Conversion Decimal/Binary Using bc

```
root@unixhost:~> bc
bc 1.06
Copyright 1991-1994, 1997, 1998, 2000 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'.
ibase=10
obase=2
7
111
quit
root@unixhost:~>
```

After the interpreter is started, the command ibase=10 tells it to treat the input, if it is a number, as decimal; this is the default. The second line obase=2 means convert the output to binary. The third line is the number 7, and after pressing Enter, it is converted to binary, which equals 111. The last command, quit, exits the interpreter. If this simple conversion is all that is needed, you have a quicker way to archive the same result, as shown in Listing 6.19.

# LISTING 6.19 Using bc with a Pipe

```
root@unixhost:~> echo "obase=2;7" | bc
111
```

echo outputs the string obase=2;7 and pipes it into bc. The ; acts as line delimiter, just like in Perl or C.

There are two versions of bc, though, the "original" one and an extended GNU version. The latter contains, among other things, the command print, which behaves a bit like the same command in Perl. The default version delivered with Solaris, for example, does not know the print command, but you can always install the GNU version, if the additional capabilities are needed.

It is even possible to write programs in bc's language. Listing 6.20 shows how to make use of that capability.

# LISTING 6.20 bc Program conv_tab.bc

```
x=0;
print "\n"
```