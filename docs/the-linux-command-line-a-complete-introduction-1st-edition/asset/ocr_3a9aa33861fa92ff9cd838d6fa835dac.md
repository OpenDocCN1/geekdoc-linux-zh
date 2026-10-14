Seeing that test and [[ ]] do roughly the same thing, which is preferable? test is traditional (and part of POSIX), whereas [[ ]] is specific to bash. It’s important to know how to use test, since it is very widely used, but [[ ]] is clearly more useful and is easier to code.

# PORTABILITY IS THE HOBGOBLIN OF LITTLE MINDS

If you talk to “real” Unix people, you quickly discover that many of them don’t like Linux very much. They regard it as impure and unclean. One tenet of Unix followers is that everything should be portable. This means that any script you write should be able to run, unchanged, on any Unix-like system.

Unix people have good reason to believe this. Having seen what proprietary extensions to commands and shells did to the Unix world before POSIX, they are naturally wary of the effect of Linux on their beloved OS.

But portability has a serious downside. It prevents progress. It requires that things are always done using “lowest common denominator” techniques. In the case of shell programming, it means making everything compatible with sh, the original Bourne shell.

This downside is the excuse that proprietary vendors use to justify their proprietary extensions, only they call them “innovations.” But they are really just lock-in devices for their customers.

The GNU tools, such as bash, have no such restrictions. They encourage portability by supporting standards and by being universally available. You can install bash and the other GNU tools on almost any kind of system, even Windows, without cost. So feel free to use all the features of bash. It’s really portable.

# Control Operators: Another Way to Branch

bash provides two control operators that can perform branching. The && (AND) and || (OR) operators work like the logical operators in the [[ ]] compound command. This is the syntax:

```
command1 && command2
```

and

```
command1 || command2
```

It is important to understand the behavior of these. With the && operator, command1 is executed and command2 is executed if, and only if, command1 is successful. With the || operator, command1 is executed and command2 is executed if, and only if, command1 is unsuccessful.