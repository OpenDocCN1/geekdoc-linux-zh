
## Table 9.23 Format Specifiers for the printf Command

| Format Specifier | Value |
|---|---|
| \" | Double quote |
| \0NNN | An octal character in which NNN represents 0 to 3 digits |
| \\ | Backslash |
| \a | Alert or beep |
| \b | Backspace |
| \c | Produce no further output |
| \f | Form feed |
| \n | Newline |
| \r | Carriage return |
| \t | Horizontal tab |
| \v | Vertical tab |
| \xNNN | Hexadecimal character in which NNN is 1 to 3 digits |
| %% | Single % |
| %b | ARGUMENT as a string with \ escapes interpreted |

## EXAMPLE 9.103

```
1 > printf --version
printf (GNU sh-utils) 1.16
2 > printf "The number is %.2f\n" 100
The number is 100.00
3 > printf "% -20s%-15s%10.2f\n" "Jody" "Savage" 28
Jody              Savage                28.00
4 > printf "%s-20s%-15s%10.2f\n" "Jody" "Savage" 28
/Jody             /Savage                28.00/
```

## EXPLANATION

+   1 The GNU version of the printf command is printed. It is found in /usr/bin.
+   2 The argument 100 is printed as a floating-point number with only two places to the right of the decimal point printing, designated by the format specification %.2f in the format string. Note that unlike C, there are no commas separating the arguments.

## EXPLANATION (CONTINUED)

3 This time the format string specifies that three conversions will take place: the first one is % -20s (a left-justified, 20-character string), next is % -15s (a left-justified, 15-character string), and last is %10.2f (a right-justified 10-character floating-point number, one of those characters is the period and the last two characters are the two numbers to the right of the decimal point). Each argument is formatted in the order of the corresponding % signs, so that string "Jody" corresponds to first %, string "Savage" corresponds to the second %, and the number 28 to the last % sign. The vertical bars are used to demonstrate the width of the fields.

## 9.19.3 Curly Braces and Variables

Curly braces insulate a variable from any characters that may follow it. They can be used to concatenate a string to the end of the variable.

## EXAMPLE 9.104

```
1 > set var = net
> echo $var
net
2 > echo $varwork
varwork: Undefined variable.
3 > echo ${var}work
network
```

## EXPLANATION

1 The curly braces surrounding the variable name insulate the variable from characters that follow it.
2 A variable called varwork has not been defined. The shell prints an error message.
3 The curly braces shield the variable from characters appended to it. $var is expanded and the string work is appended.

## 9.19.4 Uppercase and Lowercase Modifiers

A special history modifier can be used to change the case of letters in a variable.

## Table 9.24 TC Shell Case Modifiers

| Modifier | What It Does |
|---|---|
|:a | Apply a modifier as many times as possible to a single word. |
|:g | Apply a modifier once to each word. |
|:l | Lowercase the first uppercase letter in a word. |
|:u | Uppercase the first lowercase letter in a word. |

## EXAMPLE 9.105

```
1 > set name = nicky
> echo $name:u
Nicky
2 > set name = ( nicky jake )
> echo $name:gu
Nicky Jake
3 > echo $name:agu
NICKY JAKE
4 > set name = ( TOMMY DANNY )
> echo $name:ag1
tommy danny
5 > set name = "$name:agu"
> echo $name
TOMMY DANNY
```

## EXPLANATION

+   1 When :u is appended to the variable, the first letter in its value is uppercased.
+   2 When :gu is appended to the variable, the first letter in each word in the list of values is uppercased.
+   3 When :agu is appended to the variable, all letters in its value are uppercased.
+   4 When :ag1 is appended to the variable, all letters in its value are lowercased.
+   5 The variable is reset with all letters in its list uppercased.

## 9.20 TC Shell Built-In Commands

Rather than residing on disk like UNIX/Linux executable commands, built-in commands are part of the C/TC shells internal code and are executed from within the shell. If a built-in command occurs as any component of a pipeline except the last, it is executed in a sub-shell. The tcsh built-in command aptly called builtins lists all the built-in commands.

## EXAMPLE 9.106

```
1 > builtins
; @ alias alloc bg bindkey break
breaksw builtins case cd chdir complete continue
default dirs echo echo tc else end endif
endsw eval exec exit fg filetest foreach
glob goto hashstat history hug if jobs
kill limit log login logout ls-F nice
nohup notify onintr popd printenv pushd rehash
repeat sched set setenv set tc setty shift
source stop suspend switch telltc time umask
unalias uncomplete unhash unlimit unset unsetenv wait
where which while
```
