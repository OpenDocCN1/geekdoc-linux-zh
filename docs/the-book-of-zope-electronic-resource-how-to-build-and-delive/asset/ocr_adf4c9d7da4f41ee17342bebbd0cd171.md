# Table 4-9: Conditional Expression Operators

| Operator | Description | Example |
|---|---|--|
| == | True if operands are equal | "username == 'vincentp' |
| != | True if not equal | "size != 1" |
| >= | True greater than or equal to | "size >= min_size" |
| <= | True less than or equal to | "size <= max_size" |
| > | True greater than | "x > y" |
| < | True less than | "z < y" |

# Table 4-10: Logical Operators

| Operator | Description | Example |
|---|---|--|
| not | Negation: False values become true and true values become false. | "not title" (returns true if title is empty) |
| and | True only if both operands are true. | "size!=i and size<=max_size" |
| or | True if any operand is true. | "xy or zy" |

# 4.3.7 The unless Tag

Like the if, the unless tag is used to insert text subject to certain conditions, but it carries out instructions only if a defined condition is not fulfilled (is a false value). The unless tag is a non-empty block tag and accepts the name and expr attributes, using the following structure:

```
<html-unless Condition>
Instructions
</html-unless>
```

> Unlike the if, the unless tag cannot have else tags within it.

# 4.3.8 The with Tag

The with tag is used to manipulate the DTML namespace. It is very useful in the following cases:

+   * To access different variables with the same names.
* To define new variables for a short period of time in the DTML namespace.
* To access objects or properties that are not in the namespace by default because they are not in the acquisition path.