# 176

# cpp

```
#include <filename>
```

```
# Read in the contents of filename at this location. This data is
processed by cpp as if it were part of the current file. When the
<filename> notation is used, filename is searched for only in the
standard include directories. See the -I and -Y options for above more
detail. No additional tokens are permitted on the directive line after
the final "or".
```

```
#line integer-constant "filename"
```

```
Generate line control information for the next pass of the C compiler.
integer-constant is interpreted as the line number of the next line,
and filename is interpreted as the file it contains. If "filename" is
not given, the current filename is unchanged. No additional tokens
are permitted on the directive line after the optional filename.
```

```
#if constant-expression
```

```
Include subsequent lines up to the matching #else, #elif, or #endif
directive in the output only if constant-expression yields a non-zero
value. All binary assignment operators, including &&, ||, =
are legal in constant-expression. The ?: operator, and the unary -
!, and - operators are also legal in constant-expression.
```

```
The precedence of these operators is the same as that for C. In addition,
defined unary operator can be used in constant-expression in
these two forms: defined (name) or defined name. This allows the
effect of #ifdef and #endif directives in the #if directive. Only use
operators, integer constants, and names known by cpp within
constant-expression. In particular, the size of operator is not
```

```
#ifdef name
```

```
Include subsequent lines up to the matching #else, #elif, or #endif
in the output only if name has been defined either with a #define
directive or a -D option, and in the absence of an intervening #undef
directive. Additional tokens after name on the directive line are silently
ignored.
```

```
#ifdef name
```

```
Include subsequent lines up to the matching #else, #elif, or #endif
in the output only if name has not been defined or if its definition has
removed with an #undef directive. No additional tokens are
permitted on the directive line after name.
```

```
#elif constant-expression
```

```
Any number of #if directives can appear between an #if, #ifdef, or
#ifdef directive and a matching #else or #endif directive. Include
the lines following the #elif directive in the output only if all of
conditions hold.
```