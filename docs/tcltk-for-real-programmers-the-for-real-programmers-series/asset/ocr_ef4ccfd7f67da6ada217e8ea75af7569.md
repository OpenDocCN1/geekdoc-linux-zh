# Chapter 3. Introduction to the Tcl Language

The expr command is a general-purpose calculation command that will perform arbitrarily complex math operations. Unlike most Tcl commands, expr does not expect a fixed number of arguments. It can be invoked with the arguments grouped as a string or as individual values and operators. Arguments to expr may be grouped with parentheses to control the order of math operations.

The expr command can also evaluate boolean expressions and is used to test conditions by the Tcl branching and looping commands.

**Syntax:** expr mathExpression

Tcl commands support these math operations (grouped in decreasing order of precedence):

+   - ~ ! Unary minus, unary plus, bitwise NOT, logical NOT
- / % Multiply, divide, remainder
- + Add, subtract
- << >> Left shift, right shift
- > <= Less, greater than, less than or equal, greater than or equal
- != Equality, inequality
- & Bitwise AND
- ^ Bitwise exclusive OR
- | Bitwise OR
- && Logical AND. Produces a 1 result if both operands are nonzero, 0 otherwise.
- || Logical OR. Produces a 0 result if both operands are zero, 1 otherwise.

x?y:z If-then-else, as in C If x evaluates to nonzero, then the result is the value of y. Otherwise, the result is the value of z. The x operand must have a numeric value. The y and z operands may be variables or Tcl commands.