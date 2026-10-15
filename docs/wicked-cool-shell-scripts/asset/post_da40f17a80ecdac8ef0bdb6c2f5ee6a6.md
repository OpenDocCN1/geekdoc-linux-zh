
### Hacking the Script

Whatever you can do in bc on a command line you can do in this script, with the caveat that calc.sh has no line-by-line memory or state retention. This means you could add more mathematical functions to the help system, if you were so inclined. For example, the variables obase and ibase let you specify input and output numeric bases, though since there’s no line-by-line memory, you’d have to either modify scriptbc (Script #9 on page 34) or learn to enter the setting and the equation all on a single line.

## 24 Converting Temperatures

The script in Listing 3-8, which marks the first use of sophisticated mathematics in this book, can translate any temperature between Fahrenheit, Celsius, and Kelvin units. It uses the same trick of piping an equation to bc as we used in Script #9 on page 34.

### The Code

```bash
#!/bin/bash

# convertatemp--Temperature conversion script that lets the user enter
# a temperature in Fahrenheit, Celsius, or Kelvin and receive the
# equivalent temperature in the other two units as the output

if [ $# -eq 0 ]; then
    cat << EOF >&2
Usage: $0 temperature[F|C|K]
where the suffix:
    F  indicates input is in Fahrenheit (default)
    C  indicates input is in Celsius
    K  indicates input is in Kelvin
EOF
    exit 1
fi

unit="$(echo $1 | sed -e 's/-*[[:digit:]]//g' | tr '[:lower:]' '[:upper:]')"
temp="$(echo $1 | sed -e 's/[^[:digit:]]//g')"

case ${unit:-F} in
F) # Fahrenheit to Celsius formula: Tc = (F - 32) / 1.8
    fahr="$temp"
    cels="$(echo "scale=2;($fahr - 32) / 1.8" | bc)"
    kelv="$(echo "scale=2;$cels + 273.15" | bc)"
    ;;
C) # Celsius to Fahrenheit formula: Tf = (9/5)*Tc+32
    cels=$temp
    kelv="$(echo "scale=2;$cels + 273.15" | bc)"
    fahr="$(echo "scale=2;(1.8 * $cels) + 32" | bc)"
    ;;
K) # Celsius = Kelvin - 273.15, then use Celsius -> Fahrenheit formula
    kelv=$temp
    cels="$(echo "scale=2; $kelv - 273.15" | bc)"
    fahr="$(echo "scale=2; (1.8 * $cels) + 32" | bc)"
    ;;
*)
    echo "Given temperature unit is not supported"
    exit 1
    ;;
esac

echo "Fahrenheit = $fahr"
echo "Celsius     = $cels"
echo "Kelvin      = $kelv"

exit 0
```

*Listing 3-8: The convertatemp shell script*

### How It Works

At this point in the book, most of the script is probably clear, but let's have a closer look at the math and regular expressions that do all the work. "Math first," as most school-age children would undoubtedly not appreciate hearing! Here is the formula for converting degrees Fahrenheit to degrees Celsius:

C = (F - 32) / 1.8

Converted into a sequence that can be fed to bc and solved, it looks like the code at ①. The reverse conversion, Celsius to Fahrenheit, is at ①. The script also converts the temperature from Celsius to Kelvin ②. This script demonstrates one big reason to use mnemonic variable names: it makes the code a whole lot easier to read and debug.

The other bits of code here that are interesting are the regular expressions, the gnarliest of which is easily the one at ①. What we're doing is pretty straightforward, if you can unwrap the sed substitution. Substitutions always look like s/old/new/; the old pattern here is zero or more occurrences of -, followed by any of the set of digits (recall that [:digit:] is the ANSI character set notation for any digit and * matches zero or more occurrences of the previous pattern). The new pattern then is what we want to replace the old pattern with, and in this case it is simply /, which signifies an empty pattern; this pattern is useful when you just want to remove the old one. This substitution effectively removes all the digits so that inputs like -31F turn into just F, giving us the type of units. Finally, the tr command normalizes everything to uppercase so, for example, -31f turns into F.

The other sed expression does the opposite: it removes anything that isn't numeric by using the "^" operator to negate any characters in the class [:digit:]. (Most languages use ! as negation.) This provides us with the value we eventually convert using the appropriate equation.

### Running the Script

This script has a nice, intuitive input format, even if it is pretty unusual for a Unix command. Input is entered as a numeric value, with an optional suffix that indicates the units of the temperature entered; when no suffix is given, the code assumes the units are Fahrenheit.

To see the Celsius and Kelvin equivalents of 0° Fahrenheit, enter 0F. To see what 100° Kelvin is in Fahrenheit and Celsius, use 100K. And to get 100° Celsius in Kelvin and Fahrenheit, enter 100C.

You'll see this same single-letter suffix approach again in Script #60 on page 190, which converts currency values.

### The Results

Listing 3-9 shows conversion across many different temperatures.

```text
$ convertatemp 212
Fahrenheit = 212
Celsius     = 100.00
Kelvin      = 373.15
$ convertatemp 100C
Fahrenheit = 212.00
Celsius     = 100
Kelvin      = 373.15
$ convertatemp 100K
Fahrenheit = -279.67
Celsius     = -173.15
Kelvin      = 100
```

*Listing 3-9: Testing the convertatemp shell script with a few conversions*

### Hacking the Script

You can add a few input flags to generate succinct output for only one conversion at a time. Something like convertatemp -c 100F could output just the Celsius equivalent of 100° Fahrenheit, for example. This approach will help you use converted values in other scripts as well.

## 25 Calculating Loan Payments

Another common calculation users might deal with is estimation of loan payments. The script in Listing 3-10 also helps answer the question "What can I do with that bonus?" and the related question "Can I finally afford that new Tesla?"
