# ANSI character codes

You understand more than your computer understands. Hard to believe, but computers know only two numbers — ones and zeros. These numbers are known as binary numbers.

Binary numbers are ideal for doing math. The computer can use these numbers to perform calculations just as you do with your calculator. If you need letters and punctuation marks, however, your computer falls flat on its face. But thanks to the American National Standards Institute (ANSI), your computer can compare our words against its binary numbers and figure them out. The institute devised the ANSI character codes that assign each character a set of eight binary numbers. So if you type the letter A, the computer translates that A to the number 65 (the binary-number version, that is).

Now, how does your program know whether two words are the same? It subtracts the numeric representation of each letter of both words. If the result is zero, it's a match. If the first letter of both words is A, for example, the program subtracts the numeric equivalent of the letter A (65) in the second word from the numeric equivalent of the letter A (65) in the first word. The result is zero. They match.

`let Salary=3000` tells the computer to create a variable by the name of `Salary` and to assign that variable the value 3000.

`let NewSalary=2000` tells the computer to create a variable by the name of `NewSalary` and to assign it the value 2000.

`test $Salary -eq $NewSalary` tells the computer to test to determine whether the value of the `Salary` variable is equal to the value of the `NewSalary` variable. If so, `test` returns a true value; otherwise, `test` returns a false value. Finally, `echo "$?"` displays the value that `test` returns.

A true value is any value that's not zero; a false value is zero.

# The -ne (not equal to) operator

To determine whether two values aren't the same, you use the -ne operator, as in the following example:

```
let Salary=3000
let NewSalary=2000
test $Salary -ne $NewSalary
echo "$?"
```