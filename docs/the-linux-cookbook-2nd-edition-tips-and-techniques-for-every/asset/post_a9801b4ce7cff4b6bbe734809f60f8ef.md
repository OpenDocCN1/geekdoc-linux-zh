
⇒ Here are two ways to use this.

- To output the sequence of numbers from 1 to 7, type:
  $ seq 7 [RET]

- To output the sequence of numbers from 1 to -7, type:
  $ seq -7 [RET]

To output the sequence from any one number to another, give those numbers as arguments.

⇒ Here are two ways to use this.

- To output the sequence of numbers from 9 to 0, type:
  $ seq 9 0 [RET]

- To output the sequence of numbers from -1 to -20, type:
  $ seq -1 -20 [RET]

To specify an increment other than one, give it as the second argument, between the starting and ending number.

⇒ To output the sequence of numbers from -1 to 14, incrementing by 3, type:

```
$ seq -1 3 14 [RET]
```

Use the -w option to pad numbers with leading zeros so that they're all output with the same width.

Specify a separator string to be output between numbers as an argument to the -s option; the default is a newline character, which outputs each number in the sequence on its own line.

⇒ Here are two ways to use this.

- To output the sequence of numbers from 9 to 999, incrementing by 23, with numbers padded with zeros so that they're all of equal width, type:
  $ seq -w 9 23 999 [RET]

- To output the sequence of numbers from 1 to 23, with a space character between each, type:
  $ seq -s ' ' 1 23 [RET]

To pass a sequence of numbers as arguments to a command, pipe the output of seq using a space character as a separator.

⇒ To concatenate all the files in the current directory, whose names are numbers from 25 through 75, into a new file called selected-mail, type:

```
$ cat `seq -s " " 25 75` > selected-mail [RET]
```

The preceding example substitutes the output of seq as an argument to cat (see Recipe 3.1.11 [Specifying the Output of a Command as an Argument], page 65).

## 29.4 Finding Prime Factors

The factor tool calculates and outputs the prime factors of numbers passed as arguments.

⇒ To output the prime factors of 2000, type:

```
$ factor 2000 [RET]
2000: 2 2 2 2 5 5 5
$
```

NOTES: If no number is given, factor reads numbers from standard input; numbers should be separated by space, tab, or newline characters.

## 29.5 Converting Amounts and Numbers

The following recipes are for converting numbers in various ways.

### 29.5.1 Converting an Amount Between Units of Measurement

Units
DEB: units
RPM: units
WWW: http://www.gnu.org/software/units/

Use the units tool to convert a measurement from one measurement scale to another. Give two quoted arguments: the value and the name of the units you have, and the name of the units to convert to. It outputs two values: the converted value in the new units, and how much of the original measurement is equivalent to one of the new units.

⇒ To output the number of ounces in 50 grams, type:

```
$ units '50 grams' 'ounces' [RET]
    * 1.7636981
    / 0.56699046
$
```

In this example, the output indicates that there are about 1.7636981 ounces in 50 grams, and that conversely, one ounce is about 0.56699046 times 50 grams.

The units tool understands a great many different kinds of units—from Celsius and Fahrenheit to pounds, hectares, the speed of light, and a “baker’s dozen.” All understood units are kept in a text file database; use the -V option to output the location of this database on your system, and then peruse or search through it to see which units your version supports.

⇒ To determine the location of the units database, type:

```
$ units -V [RET]
units version 1.55 with readline, units database in
/usr/share/misc/units.dat
$
```

In this example, the units database is located in the file /usr/share/misc/units.dat, which is the file to peruse to list all of the units data.

NOTES: With no arguments, units runs interactively, asking you first what you have, and then second what you want.

More units of measurement can be found in A Dictionary of Units of Measurement [http://www.unc.edu/~rowlett/units/].

### 29.5.2 Converting an Arabic Numeral to English

Bsd-games
DEB: bsdgames
RPM: bsd-games
WWW: http://www.ibiblio.org/pub/Linux/games/

Use number to convert Arabic numerals to English text. Give a numeral as
