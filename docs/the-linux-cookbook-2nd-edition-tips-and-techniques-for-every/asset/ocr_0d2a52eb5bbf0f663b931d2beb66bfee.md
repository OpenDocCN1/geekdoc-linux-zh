⇒ To output the number of ounces in 50 grams, type:

```
$ units '50 grams' 'ounces' RET
    * 1.7636981
    / 0.56699046
$
```

In this example, the output indicates that there are about 1.7636981 ounces in 50 grams, and that conversely, one ounce is about 0.56699046 times 50 grams.

The units tool understands a great many different kinds of units—from Celsius and Fahrenheit to pounds, hectares, the speed of light, and a “baker’s dozen.” All understood units are kept in a text file database; use the -V option to output the location of this database on your system, and then peruse or search through it to see which units your version supports.

⇒ To determine the location of the units database, type:

```
$ units -V RET
units version 1.55 with readline, units database in
/usr/share/misc/units.dat
$
```

In this example, the units database is located in the file /usr/share/misc/units.dat, which is the file to peruse to list all of the units data.

NOTES: With no arguments, units runs interactively, asking you first what you have, and then second what you want.

More units of measurement can be found in A Dictionary of Units of Measurement [http://www.unc.edu/~rowlett/units/].

# 29.5.2 Converting an Arabic Numeral to English

Bsd-games
DEB: bsdgames
RPM: bsd-games
WWW: http://www.ibiblio.org/pub/Linux/games/

Use number to convert Arabic numerals to English text. Give a numeral as