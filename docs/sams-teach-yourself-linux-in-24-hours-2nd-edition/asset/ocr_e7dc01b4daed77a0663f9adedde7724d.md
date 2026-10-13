```
/ 0.0015625
You have: mile^2
You want: acre
* 640
/ 0.0015625
You have: mile
You want: furlong
* 8
/ 0.125
You have: 100 fathoms
You want: feet
* 600
/ 0.0016666667
...
```

In the interactive mode, you can ask units for any number of conversions. The units command works by reading its database of conversions from the file /usr/share/units.dat. You can also copy this file to your home directory and add your own custom conversions to it. As you can see, you can use different notations to indicate amounts to be converted. Another interesting feature is that units can also perform currency conversions, for example:

```
# units dollar yen
* 107.52688
/ 0.0093
```

Note that this might not be entirely true, as currency values change daily. You can edit the units.dat file and insert not only current currency values, but also prices for gold, silver, platinum, or pork bellies. See the units manual page for more information.

# Programming Calculators with the bc Language Interpreter

The bc command is an interpreter for a calculator language. You can use this command, by Philip Nelson, to write calculator programs while bc is running or have bc run the program after it starts. The bc language has nearly 40 operators, functions, and programming logic keywords. Although this section doesn’t go into how to program in bc, if you’re interested in the bc language, try the simple checkbook balancing program from bc’s manual page. The program can work like the previous example for the dc command. Read the bc manual page, and then type the program into a file using your favorite text editor. You can run it with the following:

```
# bc nameofyourfile
```