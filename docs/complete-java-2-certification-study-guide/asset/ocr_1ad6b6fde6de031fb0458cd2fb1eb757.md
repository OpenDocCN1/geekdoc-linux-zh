# TABLE 2.6 The AND Operation on boolean Values (continued)

| Op1 | Op2 | Op1 AND Op2 |
| true | false | false |
| true | true | true |

# TABLE 2.7 The XOR Operation on boolean Values

| Op1 | Op2 | Op1 XOR Op2 |
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | false |

# TABLE 2.8 The OR Operation on boolean Values

| Op1 | Op2 | Op1 OR Op2 |
| false | false | false |
| false | true | true |
| true | false | true |
| true | true | true |

> As with all operations, the two operands must be of compatible types. So, if either operand is of boolean type, both must be. Java does not permit you to cast any type to boolean; instead you must use comparisons or methods that return boolean values.

The next section covers the short-circuit logical operators. These operators perform logical AND and OR operations but are slightly different in implementation from the operators just discussed.