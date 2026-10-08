There are many conditions that the **test** command can test. Table 11-1 shows some of the more common conditions for which you can test.

# **Table 11-1 test Command Conditions**

**String tests:**

| Condition | Description |
| :--- | :--- |
| `[ "$a" = "string" ]` | True if $a is equal to “string” |
| `[ "$a" != "string" ]` | True if $a is NOT equal to “string” |
| `[ -z "$a" ]` | True if $a is null (zero characters) |
| `[ -n "$a" ]` | True if $a is NOT null |

**Numeric tests:**

| Condition | Description |
| :--- | :--- |
| `[ $x -eq 1 ]` | True if $x is equal to 1 |
| `[ $x -ne 1 ]` | True if $x is NOT equal to 1 |
| `[ $x -lt 1 ]` | True if $x is less than 1 |
| `[ $x -gt 1 ]` | True if $x is greater than 1 |
| `[ $x -le 1 ]` | True if $x is less than or equal to 1 |
| `[ $x -ge 1 ]` | True if $x is greater than or equal to 1 |

**File tests:**

| Condition | Description |
| :--- | :--- |
| `[ -d $file ]` | True if $file is a directory |
| `[ -f $file ]` | True if $file is a file |
| `[ -s $file ]` | True if $file is a file with > 0 bytes |
| `[ -r $file ]` | True if $file is readable |
| `[ -w $file ]` | True if $file is writable |
| `[ -x $file ]` | True if $file is executable |


Tests can be combined using **-a** to logically “AND” the tests together, **-o** to logically “OR” two tests, and **!** to “negate” a test. For example, this test statement is true only if the $Interactive variable is set to true or $file is a directory: