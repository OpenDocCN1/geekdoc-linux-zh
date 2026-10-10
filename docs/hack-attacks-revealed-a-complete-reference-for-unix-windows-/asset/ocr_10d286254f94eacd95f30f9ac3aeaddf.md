modes; the second mode command redirects the computer's parallel printer output to the asynchronous communication port specified in the first mode command.

For example, if your serial printer operates at 4800 baud with even parity, and if it is connected to the COM1 port, type:

```
mode com1:48,e,,p
mode lpt1:=com1:
```

If you want your computer to print on a parallel printer that is connected to your computer's second parallel printer port (LPT2), and you want to print with 80 characters per line and 8 characters per inch, type:

```
mode lpt2: 80,8
```

or

```
mode lpt2:,8
```

# More

More sends output to the console one screen at a time.

# Syntax

```
more <source
```

Where source is a file or command.

# Example

Suppose you have a long file called *paper.doc* that you want to view on your screen. The following command redirects the file through the more command to show the file's contents one screen at a time:

```
more <paper.doc
```

# Nlsfunc

Nlsfunc loads country-specific information.

# Syntax

```
nlsfunc[[drive:][path]filename]
```

Where filename specifies the file containing country-specific information.

# Comments

The default value of filename is your *config.sys* file. If no country command exists in your *config.sys* file, DOS uses the *country.sys* file in your root directory for information.

# Example