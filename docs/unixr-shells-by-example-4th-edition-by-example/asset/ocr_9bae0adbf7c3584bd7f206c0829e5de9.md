rather than part of a pattern, it too must be enclosed in quotes. The logical operators && (AND) and || (OR) replace the -a and -o operators used with the simple test command. (See Example 14.17.)

**Table 14.3 The test Command Operators**

| Test Operator | Tests True If |
|---|---|
| *String Test* | |
| `[ string1 = string2 ]`<br>`[ string1==string2 ]` | String1 is equal to String2 (*space surrounding = required*).<br>(Can be used instead of the single = sign on bash versions 2.x.) |
| `[ string1 != string2 ]` | String1 is not equal to String2 (*space surrounding != required*). |
| `[ string ]` | String is not null. |
| `[ -z string ]` | Length of string is zero. |
| `[ -n string ]` | Length of string is nonzero. |
| `[ -l string ]` | Length of string (number of characters). |
| *Logical Test* | |
| `[ string1 -a string2 ]` | Both string1 and string2 are true. |
| `[ string1 -o string2 ]` | Either string1 or string2 is true. |
| `[ ! string1 ]` | Not a string1 match. |
| *Logical Test (Compound Test)* | |
| `[[ pattern1 && pattern2 ]]` | Both pattern1 and pattern2 are true. |
| `[[ pattern1 || pattern2 ]]` | Either pattern1 or pattern2 is true. |
| `[[ ! pattern ]]` | Not a pattern match. |
| *Integer Test* | |
| `[ int1 -eq int2 ]` | Int1 is equal to int2. |
| `[ int1 -ne int2 ]` | Int1 is not equal to int2. |
| `[ int1 -gt int2 ]` | Int1 is greater than int2. |
| `[ int1 -ge int2 ]` | Int1 is greater than or equal to int2. |

```
test -n $word  or  [ -n $word ]
test tom = sue  or  [ tom = sue ]
```