function being used in the program.  
Example

```
d
```

If this program does not # the < file, this will generate an error that $ is undefined.

+   **16.** *Leaving a blank space between the name of a macro and its argument list in the # statement.*

*Example*

![](bbox=[0.01, 0.22, 0.25, 0.24])

```
#
```

This definition is incorrect, as the preprocessor considers the first blank space after the defined name as the start of the definition for that name. In this case, the statement `n` gets expanded by the preprocessor into `m` which is obviously not what is intended.

![](bbox=[0.01, 0.38, 0.25, 0.4])

+   **17.** *Using an expression that has side effects in a macro call.*

*Example*

![](bbox=[0.01, 0.52, 0.25, 0.54])

```
#
```

```
v
```

The invocation of the `$` macro causes `v` to be incremented *twice* because this statement is expanded by the preprocessor to `v`