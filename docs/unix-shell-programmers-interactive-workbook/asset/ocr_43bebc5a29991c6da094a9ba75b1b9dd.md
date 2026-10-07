# Chapter 10: Patterns, Expansions, and Substitutions 471

# LAB 10.3

Finally, there is also a set of parameter expansions that you can use to work with a subset of positional parameter lists (the special variables (@) and (*) that you covered in Exercise 5.1.3, "Use Special Parameter Variables (# @ *)", indexed arrays, and associative arrays, covered in Lab 6.2, "Arrays and Compound Variables." The syntax is analogous to the substring syntax you looked at in Question b of this exercise.

Enter the following commands:

```
integer i=( 99 88 77 66 55 )
typeset -A a
a[aa]=99 a[bb]=88 a[cc]=77 a[dd]=66 a[ee]=55
set 99 88 77 66 55
print $@ '\
' ${@:1:2}
print ${a[@]}\ '\
' ${a[@]:1:2}
print ${i[@]}\ '\
' ${i[@]:1:2}
```

g) Explain the outputs of the three print commands.