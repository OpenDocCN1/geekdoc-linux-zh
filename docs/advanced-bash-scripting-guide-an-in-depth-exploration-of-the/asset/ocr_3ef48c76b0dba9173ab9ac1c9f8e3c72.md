# Advanced Bash-Scripting Guide

+   * Null string, testing for
* Protecting strings from expansion and/or reinterpretation, *script example*

Unprotecting strings, *script example*
* *strchr()*, equivalent of
* *strlen()*, equivalent of
* *strings* command, find printable strings in a binary or data file
* Substring extraction

```
$${string:position}
```

```
$${string:position:length}
```

+   Using expr
* Substring index (numerical position in string)
* Substring matching, using expr
* Substring removal

```
$${var#Pattern}
```

```
$${var##Pattern}
```

```
$${var%%Pattern}
```

+   $${var%#Pattern}
* Substring replacement

```
$${string/substring/replacement}
```

```
$${string//substring/replacement}
```

```
$${string/##substring/replacement}
```

```
$${string/%#substring/replacement}
```

Script example

+   * **Table** of string/substring manipulation and extraction operators

**Strong quoting ‘ ... ’'

Subshell

+   * Command list within parentheses
* **Variables**, $BASH_SUBSHELL and $SHLV
* Variables in a *subshell*

scope limited, but ...n... can be accessed outside the subshell?

# Appendix T. ASCII Table