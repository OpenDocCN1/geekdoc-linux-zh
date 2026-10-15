![](bbox=[0.102, 0.091, 0.972, 0.301])

# EXPLANATION

If the pattern eastern is matched on a line, the n command causes sed to get the next line of input (the line with AM Main Jr.), replace the pattern space with this line, substitute AM with Archie, print the line, and continue.

# 5.9.12  Transform: The y Command

The y command is a transform command. It is similar to the UNIX/Linux tr command. Characters are translated on a one-to-one, corresponding basis from those on the left-hand side to those on the right-hand side. For example, in the command y/abc/ABC/ any lowercase letter a will be transformed to an uppercase A, as will b to B, and c to C.

![](bbox=[0.102, 0.556, 0.969, 0.793])

# EXPLANATION

For lines 1 through 3, the y command translates all lowercase letters to uppercase letters. Regular expression metacharacters do not work with this command, and like the substitution delimiter, the forward slash can be changed to a different character.