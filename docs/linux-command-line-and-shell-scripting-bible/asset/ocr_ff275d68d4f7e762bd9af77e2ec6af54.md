# Mathematical Operations

All of the shells allow you to perform some level of mathematical operations within them. This is the area where ksh93 and zsh shine.

The bash and dash shells use the expr command to evaluate a mathematical expression:

```
$ expr 1 + 5
6
```

They also provide the [ ] and $(()) shortcuts for defining mathematical operations:

```
$ var1=[1 + 5]
$ echo $var1
6
```

The tcsh shell uses the symbol for defining mathematical operations:

```
$ set test1 = 10
$ set test2 = 15
$ @ test3 = ($test1 * $test2)
$ echo $test3
150
$ 
```

The bash, dash, and tcsh shells can only perform integer mathematical operations.

Both ksh93 and zsh shells use two methods for defining mathematical operations. The let command:

```
% let value1="4 * 5.1 / 3.2"
% echo $value1
6.3749999999999991
```

and the $(()) shortcut:

```
% value1=$((4 * 5.1))
% ((value2 = 4 * 5.1))
% printf "%6.3f\n" $value1.$value2
20.400
20.400
%
```

Also, both the ksh93 and zsh shells fully support floating-point arithmetic in all mathematical operations.