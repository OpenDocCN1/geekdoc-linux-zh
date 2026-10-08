# Advanced Bash-Scripting Guide

units
This utility converts between different units of measure. While normally invoked in interactive mode, units may find in a script.

# Example 16-63. Converting meters to miles

```
#!/bin/bash
# unit-conversion.sh utility installed.
# Must have 'units' units

convert_units () # Takes as arguments the units to convert.
{
  cf=$$(units "$1" "$2" | sed --silent -e 'lp' | awk 'print $2')
  # Strip everything except the actual conversion factor.
  echo "$cf"
}
Unit1=miles
Unit2=meters
factor=convert_units $Unit1 $Unit2
quantity=3.73

result=$(echo $quantity | bc)
echo "There are $result $Unit2 in $quantity $Unit1."

# What happens if you pass incompatible units,
#+ such as "acres" and "miles" to the function?

echo 0

# Exercise: Edit this script to accept command-line parameters,
#  with appropriate error checking, of course.
```

m4
A hidden measure, m4 is a powerful macro [87] processing filter, virtually a complete language. Although originally written as a pre-processor for RatFor, m4 turned out to be a stand-alone utility. In fact, m4 combines the functionality of eval, tr, and awk, in addition to its extensive macro expansion facilities.

The April, 2002 issue of Linux Journal has a very nice article on m4 and its uses.

# Example 16-64. Using m4

```
#!/bin/bash
# m4.sh: Using the m4 macro processor

# Strings
string=abcdA01
echo len($string) | m4              # 7
echo substr($string, 4) | m4      # A01
echo regexp($string, [0-1],\|&Z) | m4  # 01Z

# Arithmetic
var=99
echo incr($var) | m4                  # 100
```

Chapter 16. External Filters, Programs and Commands 316