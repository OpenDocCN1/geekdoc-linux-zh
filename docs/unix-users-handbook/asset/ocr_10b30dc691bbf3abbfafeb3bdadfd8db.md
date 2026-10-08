# # Constants

We’ve previously discussed the concept of a variable, a place in the computer memory that has a name and contents that can be changed. A constant is also a value stored in computer memory, but the value cannot be changed.

A constant can be assigned to a variable, but you can not assign new values to a constant. Below is an example of how a constant can be assigned to variables:

```
```python
pens = 10;
```
```

This shows how the constant 10 can be assigned to the variable pens. Essentially, the value of 10 has been placed in the pens variable.

There are a few types of constants. An integer constant can be formed using the digits 0 through 9. The character constants are enclosed within single quotes (‘Z’). Floating-point constants use the digits 0 through 9 and a decimal point.

# # Symbolic Constants

Symbolic constants are names or identifiers that can be used in a program instead of the actual value of a constant. When the program is compiled, the preprocessor searches the source code for every occurrence of the symbolic constant identifier and substitutes it with the actual constant value.

The define directive is used to create a symbolic constant. The define directive is a preprocessor directive that assigns a name or identifier to the constant. Preprocessor directives are statements beginning with a pound sign (#). The define directive consists of #define followed by an identifier and then a constant. The following directive defines a symbolic constant for the value of pi: