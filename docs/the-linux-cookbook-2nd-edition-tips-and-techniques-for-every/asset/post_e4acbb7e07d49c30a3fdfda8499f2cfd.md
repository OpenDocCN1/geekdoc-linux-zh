
For example, suppose you have a file `temperature2.data`, as in Figure 29-5.

```
#Month	Honolulu	Tampa	New York
January	73	60	32
February	73	61	33
March	74	66	41
April	76	72	53
May	78	77	62
June	79	81	71
July	80	82	77
August	81	82	75
September	81	81	68
October	80	74	58
November	77	67	47
December	74	61	36
```

Figure 29-5. The temperature2.data file.

This file contains four columns of text, delimited by tab characters. The first line is a comment—any lines beginning with a pound-sign character (#), in either input data or gnuplot command files, are considered comments and are ignored by gnuplot

Now suppose you also have a file `temperature2.gnuplot`, as in Figure 29-6.

```
set title "Mean Monthly Temperatures for Company Locations"
set xlabel "Month"
set ylabel "Temperature"
set xdata time
set timefmt "%B"
set format x "%b"
set nomxtics
set terminal postscript landscape color
set output "temps2.ps"
plot "temperature2.data" using 1:2 title "Honolulu" with linespoints, "" using 1:3 title "Tampa" with linespoints, "" using 1:4 title "New York" with linespoints
```

Figure 29-6. The temperature2.gnuplot file.

This is very similar to the command file in the previous example, except for the following differences: The title is changed; the command to turn off the key is not printed; the name of the output file differs; and in the long last plot line, columns two through three are each plotted against the first column (the month names) in the input file, each with the linespoints style as before, but each with its own label for the key.

⇒ To process the commands in temperature2.gnuplot, type:

```
$ gnuplot temperature.gnuplot [RET]
```

This command starts gnuplot and runs the commands in the file temperature2.gnuplot. A new PostScript file, temps2.ps, is written, which looks like Figure 29-7. (While the printed illustration is in black and white, the actual image created from this command has colored plots.)

![](img/be7f02611e5cefde1a18c788fede22f7_612_0.png)

Figure 29-7. The temps2.ps file.

## 29.9 Using Other Mathematics Tools

The following table lists some of the other more popular mathematics-related tools available for Linux.

### Calc

Scientific calculator tool for Emacs.
DEB: calc
RPM: calc
WWW: http://www.isthe.com/chongo/tech/comp/calc/

### Desk Calculator

Arbitrary-precision calculator that reads from standard input and writes to standard output. DC is a reverse-polish calculator; that is, numbers are pushed on a last-in first-out (LIFO) list called a stack. When you give an arithmetic operation symbol, DC pops numbers off the stack for their operands, and then it pushes the evaluation on the stack. Very useful for getting evaluations in scripts and at the command line.
DEB: dc
WWW: http://www.cypherspace.org/~adam/rsa/dc.html

### Dome

Calculates the properties of a geodesic dome—chord factors, spherical vertex coordinates, and so on. Supports "Buckyball" formations and elliptical geodesics, and generates plain text output as well as formats for spreadsheets, CAD, and ray-tracing tools.
DEB: dome
WWW: http://tinyurl.com/2p5b4

### GnuCash

Intuitive personal finance application, used for managing finances (including bank accounts, stocks, income, and expenses); it's "based on professional accounting principles" to ensure accuracy in computation and reporting.
DEB: gnucash
RPM: gnucash
WWW: http://www.gnucash.org/

### Gnumeric

Powerful spreadsheet application for GNOME that is somewhat reminiscent of Excel.
DEB: gnumeric
RPM: gnumeric
WWW: http://www.gnome.org/projects/gnumeric/

### Oleo

Small GNU spreadsheet application that can run in both an X window and in terminals, has Emacs-like key bindings, and can generate PostScript output.
DEB: oleo
RPM: oleo
WWW: http://www.gnu.org/software/oleo/

### Piechart

Facilitates making graphical pie charts with the GNU plotting utilities (below).
WWW: http://tinyurl.com/jdi6

### Plotutils

Package of GNU programs for plotting data, including GNU replacements for the old UNIX standbys of graph, plot, and spline.
DEB: plotutils
RPM: plotutils
WWW: http://tinyurl.com/3eygd

### Sc

Spreadsheet tool that runs in the console; even smaller than Oleo, it provides formulas and other basic features you would expect from a minimal spreadsheet.
DEB: sc

### Sieb

Fast C program for computing prime numbers.
WWW: http://bytesex.org/misc.html

### Xcalc

Visual scientific calculator for the X Window System—it draws a calculator on the screen, and you can use the mouse or keyboard to use it. It is capable of emulating the TI-30 and HP-10C calculators.
DEB: xbase-clients
RPM: XFree86-tools

### Xspread

X client front-end to sc.
RPM: xspread
