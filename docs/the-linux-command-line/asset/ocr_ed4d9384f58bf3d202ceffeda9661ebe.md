months (15 years). Notice the precision of the answer. This is determined by the value given to the special scale variable in the bc script. A full description of the bc scripting language is provided by the bc man page. While its mathematical notation is slightly different from that of the shell (bc more closely resembles C), most of it will be quite familiar, based on what we have learned so far.

# Summing Up

In this chapter, we have learned about many of the little things that can be used to get the “real work” done in scripts. As our experience with scripting grows, the ability to effectively manipulate strings and numbers will prove extremely valuable. Our loan-calc script demonstrates that even simple scripts can be created to do some really useful things.

# Extra Credit

While the basic functionality of the loan-calc script is in place, the script is far from complete. For extra credit, try improving the loan-calc script with the following features:

+   - Full verification of the command line arguments
+   - A command line option to implement an “interactive” mode that will prompt the user to input the principal, interest rate, and term of the loan.
+   - A better format for the output.

# Further Reading

+   - The *Bash Hackers Wiki* has a good discussion of parameter expansion: http://bash-hackers.org/wiki/doku.php/syntax/pe
+   - The *Bash Reference Manual* covers this, too: http://www.gnu.org/software/bash/manual/bashref.html#Shell-Parameter-Expansion
+   - The *Wikipedia* has a good article describing bit operations: http://en.wikipedia.org/wiki/Bit_operation
+   - and an article on ternary operations: http://en.wikipedia.org/wiki/Ternary_operation
+   - as well as a description of the formula for calculating loan payments used in our loan-calc script: http://en.wikipedia.org/wiki/Amortization_calculator