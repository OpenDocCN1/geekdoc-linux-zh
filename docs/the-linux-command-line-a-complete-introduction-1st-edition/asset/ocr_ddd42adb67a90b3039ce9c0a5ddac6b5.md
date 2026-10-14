Notice that we use less-than and greater-than signs and that == is used to test for equivalence. This is a more natural-looking syntax for working with integers. Notice too, that because the compound command (( )) is part of the shell syntax rather than an ordinary command, and it deals only with integers, it is able to recognize variables by name and does not require expansion to be performed.

# Combining Expressions

It’s also possible to combine expressions to create more complex evaluations. Expressions are combined by using logical operators. We saw these in Chapter 17, when we learned about the find command. There are three logical operations for test and [[ ]]. They are AND, OR, and NOT. test and [[ ]] use different operators to represent these operations, as shown in Table 27-4.

Table 27-4: Logical Operators

| Operation | test | [[ ]] and (( )) |
|-----------|------|-----------------|
| AND       | -a   | &&              |
| OR        | -o   | ||              |
| NOT       | !    | !               |

Here’s an example of an AND operation. The following script determines if an integer is within a range of values:

```
#!/bin/bash

# test-integer3: determine if an integer is within a
# specified range of values.

MIN_VAL=1
MAX_VAL=100

INT=50

if [[ "$INT" =~ ^[0-9]+$ ]]; then
    if [[ INT -ge MIN_VAL && INT -le MAX_VAL ]]; then
        echo "$INT is within $MIN_VAL to $MAX_VAL."
    else
        echo "$INT is out of range."
    fi
else
    echo "INT is not an integer." >&2
    exit 1
fi
```