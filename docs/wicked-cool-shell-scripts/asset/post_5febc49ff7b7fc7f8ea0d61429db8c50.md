
## Running the Script

To run the script (as Listing 1-15 shows), enter a date into the command line in month-day-year format. The month can be a three-letter abbreviation, a full word, or a numeric value; the year must be four digits.

## The Results

```
$ valid-date august 3 1960
Valid date: Aug 3 1960
$ valid-date 9 31 2001
valid-date: bad day value: Sep doesn’t have 31 days.
$ valid-date feb 29 2004
Valid date: Feb 29 2004
$ valid-date feb 29 2014
valid-date: 2014 is not a leap year, so Feb doesn’t have 29 days.
```

Listing 1-15: Testing the valid-date script

## Hacking the Script

A similar approach to this script could validate time specifications, using either a 24-hour clock or an ante meridiem/post meridiem (AM/PM) suffix. Split the value at the colon, ensure that the minutes and seconds (if specified) are between 0 and 60, and then check that the first value is between 0 and 12 if allowing AM/PM, or between 0 and 24 if you prefer a 24-hour clock. Fortunately, while there are leap seconds and other tiny variations in time to help keep the calendar balanced, we can safely ignore them on a day-to-day basis, so there’s no need to fret over implementing such hairy time calculations.

A very different way to test for leap years is a possibility if you have access to GNU date on your Unix or GNU/Linux implementation. Test by specifying this command and seeing what result you get:

```
$ date -d 12/31/1996 +%j
```

If you have the newer, better version of date, you’ll see 366. In the older version, well, it’ll just complain about the input format. Now think about that result from the newer date command and see if you can figure out a two-line function that tests whether a given year is a leap year!

Finally, this script is quite permissive about month names; febmana works just fine since the case statement at ① checks only the first three letters of the specified word. This can be cleaned up and improved if you’d prefer by either testing for common abbreviations (like feb) along with the fully spelled out month name (february) and perhaps even common misspellings (febuary). All are easily done if you’re so motivated!

## #8 Sidestepping Poor echo Implementations

As mentioned in "What Is POSIX?" on page 10, while most modern Unix and GNU/Linux implementations have a version of the echo command that knows the -n flag should suppress trailing newlines on the output, not all implementations work that way. Some use \c as a special embedded character to defeat this default behavior, and others simply insist on including the trailing newline regardless.
Figuring out whether your particular echo is well implemented is easy: Simply enter these commands and see what happens:

```
$ echo -n "The rain in Spain"; echo " falls mainly on the Plain"
```

If your echo works with the -n flag, you'll see output like this:

```
The rain in Spain falls mainly on the Plain
```

If it doesn't, you'll see output like this:

```
-n The rain in Spain
falls mainly on the Plain
```

Ensuring that the script output is presented to the user as desired is important and will become increasingly important as our scripts become more interactive. To that end, we'll write an alternate version of echo, called echon, that will always suppress the trailing newline. That way we'll have something reliable to call every time we want the echo -n functionality.

## The Code

There are as many ways to solve this quirky echo problem as there are pages in this book. One of our favorites is very succinct; it simply filters its input through the awk printf command, as Listing 1-16 shows.

```
echon()
{
  echo "$s" | awk '{ printf "%s", $0 }'
}
```

Listing 1-16: A simple echo alternative using the awk printf command

However, you may prefer to avoid the overhead incurred when calling the awk command. If you have a user-level printf command, you can write echon to filter input through that instead, as in Listing 1-17.

```
echon()
{
  printf "%s" "$s"
}
```

Listing 1-17: An echo alternative using a simple printf command
