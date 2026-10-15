# 10.6.7 The if Statement and a Single Command

If an expression is followed by a single command, the then and endif keywords are not necessary.

# FORMAT

```
if ( expression ) single command
```

# EXAMPLE 10.16

```
if ($#argv == 0) exit 1
```

# EXPLANATION

The expression is tested. If the number of command-line arguments, $#argv, is equal to 0, the program is exited with a status of 1.

# 10.6.8 The if/else if Statement

The if/else if construct offers a multiway decision-making mechanism. A number of expressions can be tested, and when one of the expressions evaluated is true, the block of statements that follow is executed. If none of the expressions is true, the else block is executed.

# FORMAT

```
if ( expression ) then
  command
  command
else if ( expression ) then
  command
  command
else
  command
endif
```

# EXAMPLE 10.17