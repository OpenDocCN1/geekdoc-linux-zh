# Table 2.1 C and TC Shell Syntax and Constructs (continued)

| Conditional statements (continued) | The switch construct is:
switch variable_name
case constant1:
  statements
case constant2:
  statements
case constant3:
  statements
default:
  statements
endsw | switch "$color" )
case blue:
  echo $color is blue
  breaksw
case green:
  echo $color is green
  breaksw
case red:
  case orange:
  echo $color is red or orange
  breaksw
default:
  echo "Not a valid color"
endsw |

| Loops | There are two types of loops, the while and foreach loop.

The while loop is followed by an expression enclosed in parentheses, a block of statements, and terminated with the end keyword. As long as the expression is true, the looping continues.

The foreach loop is followed by a variable name and a list of words enclosed in parentheses, a block of statements, and terminates with the end keyword. The foreach loop iterates through a list of words, processing a word and then shifting it off, then moving to the next word. When all words have been shifted from the list, it ends.

The loop control commands are break and continue.

EXAMPLE

while ( expression )
  block of statements
end

foreach variable ( word list )
  block of statements
end
----------------------------
foreach color (red green blue)
  echo $color
end |

| File testing | The C shell has a built-in set of options for testing attributes of files, such as whether it is a directory, a plain file (not a directory), a readable file, and so forth. For other types of file tests, the UNIX test command is used. See Example 2.1 for a demonstration. |