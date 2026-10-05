# CHAPTER 27 PROGRAMMING THE BOURNE SHELL

The Boolean AND operator (&&) produces a result of 1 if both of its operands are nonzero and a result of 0 otherwise. The bitwise inclusive OR operator (|) selects the bits that are on either 0101 or 0110, resulting in 0111, which is 7 decimal. The Boolean OR operator (||) produces a result of 1 if either of its operands is non-zero and a result of 0 otherwise.

```
$ echo $((v1 && v2))
1
$ echo $((v1 | v2))
7
$ echo $((v1 || v2))
1
```

Next the bitwise exclusive OR operator (^) selects the bits that are on either, but not both, of operands 0101 and 0110, yielding 0011, which is 3 decimal. The Boolean NOT operator (!) produces a result of 1 if its operand is 0 or a result of 0 otherwise. The exclamation point in $(( ! v )) is enclosed within double parentheses, it does not need to be escaped to prevent the shell from interpreting the exclamation point as a history event. The comparison operators produce a result of 1 if the comparison is true and a result of 0

```
$ echo $((v1 ^ v2))
3
$ echo $(( ! v ))
0
$ echo $((v1 < v2))
1
$ echo $((v1 > v2))
0
```

# SHELL PROGRAMMING

The Bourne Again Shell has many features that make it a good programming language. The structures that bash provides are not a random assortment, but rather have been chosen to provide most of the structural features that are found in other procedural languages, such as C or Perl. procedural language provides the following abilities:

+   * Declare, assign, and manipulate variables and constant. The Bourne Again Shell provides string variables, together with powerful string operators, and integer variables, along with a complete set of arithmetic operators.
* Break large problems into small ones by creating subprograms. The Bourne Again Shell allows you to create functions and call scripts from other scripts. Shell functions can be called recursively; that is, a Bourne Again function can call itself. You may not need to use recursion, but it may allow you to solve some apparently difficult problems with ease.
* Execute statements conditionally, using statements such as if.
* Execute statements iteratively, using statements as while and for.