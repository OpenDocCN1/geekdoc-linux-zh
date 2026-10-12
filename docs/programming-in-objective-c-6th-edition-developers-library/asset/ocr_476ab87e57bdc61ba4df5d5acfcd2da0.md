# 9.2.2 The `#error` Directive

The general format for declaring the `#` directive is as follows:

```
```
# text
```
```

The specified *text* is written as an error message by the preprocessor.

# 9.2.3 The `#if` Directive

One general format for declaring the `#` directive is as follows:

```
```
#
```
```

The value of *constant\_expression* is evaluated. If the result is nonzero, all program lines up until the `#` directive are processed; otherwise, they are automatically skipped and are not processed by the preprocessor or by the compiler.

Another general format for declaring the `#` directive is as follows:

```
```
# constant_expression_1
# constant_expression_2
# constant_expression_n
#
# 
```
```

If *constant\_expression* is nonzero, all program lines up until the `#` are processed, and the remaining lines up to the `#` are skipped. Otherwise, if *constant\_expression* is nonzero, all program lines up until the next `#` are processed, and the remaining lines up to the `#` are skipped. If none of the constant expressions evaluates to nonzero, the lines after the `#` (if included) are processed.

The special operator `defined` can be used as part of the constant expression, so

```
```
#
# 
```
```

causes the code between the `#` and `#` to be processed if the identifier `defined` has been previously defined (see [Section 9.2.4](#9.2.4)). The parentheses are not necessary around the identifier, so

```
```
# 
```
```

works just as well.

# 9.2.4 The `#ifdef` Directive

The general format for declaring the `#` directive is as follows:

```
```
# identifier
#
```
```

If the value of *identifier* has been previously defined (either through a `#` or with the `-` command-line option when the program was compiled), all program lines up until the `#` are