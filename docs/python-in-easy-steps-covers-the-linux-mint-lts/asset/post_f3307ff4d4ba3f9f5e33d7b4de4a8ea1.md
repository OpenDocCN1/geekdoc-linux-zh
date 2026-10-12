
There and run this program – to see the result of the arithmetical operations

![](img/d06b1f1cf83677f6647237f0c7827141_38_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_38_1.png)

The `\t` escape sequence shown here adds an invisible tab character to format the output.

![](img/d06b1f1cf83677f6647237f0c7827141_38_2.png)

You can use the **sep** parameter to explicitly specify the separation between output – here it specifies no spaces by assigning two unspaced single quote marks.

## Assigning values

The operators that are used in Python programming to assign values are listed in the table below. All except the simple = assignment operator are a shorthand form of a longer expression, so each equivalent is given for clarity:

| Operator: | Example: | Equivalent: |
| :--- | :--- | :--- |
| = | a = b | a = b |
| += | a += b | a = (a + b) |
| -= | a -= b | a = (a - b) |
| *= | a *= b | a = (a * b) |
| /= | a /= b | a = (a / b) |
| %= | a %= b | a = (a % b) |
| //= | a //= b | a = (a // b) |
| **= | a **= b | a = (a ** b) |

In the example above, the variable named “a” is assigned the value that is contained in the variable named “b” – so that becomes the new value stored in the a variable.

![](img/d06b1f1cf83677f6647237f0c7827141_39_0.png)

It is important to regard the = operator to mean “assign” rather than “equals” to avoid confusion with the == equality operator.

The `+=` operator is useful to add a value onto an existing value that is stored in the `a` variable.

In the table example, the `+=` operator first adds the value contained in variable `a` to the value obtained in variable `b`. It then assigns the result to become the new value stored in variable `a`.

All the other operators work in the same way by making the arithmetical operation between the two values first, then assigning the result of that operation to the first variable – to become its new stored value.

With the `%=` operator, the first operand `a` is divided by the second operand `b`, then the remainder of that operation is assigned to the `a` variable.

- Start a new Python script that initializes two variables by assigning integer values and displays both assigned values

```python
a = 8
b = 4
print( 'Assign Values:\t\t', 'a =', a, '\tb =', b )
```

![](img/d06b1f1cf83677f6647237f0c7827141_40_0.png)

- Next, add and assign a new value to the first variable and display its stored value

```python
a += b
print( 'Add & Assign:\t\t', 'a =', a , '(8 + 4)' )
```

- Now, subtract and assign a new value to the first variable and display its stored value, then multiply and assign a value to the first variable and display its stored value

```python
a -= b
print( 'Subtract & Assign:\t', 'a =', a , '(12 - 4)' )

a *= b
print( 'Multiply & Assign:\t', 'a =', a , '(8 x 4)' )
```

- Finally, divide and assign a new value to the first variable and display its stored value, then modulo and assign a value to the first variable and display its stored value

```python
a /= b
print( 'Divide & Assign:\t' , 'a =', a, '(32 ÷ 4)' )

a %= b
print( 'Modulo & Assign:\t' , 'a =', a, '(8 % 4)' )
```

- Save the file in your scripts directory, then open a Command Prompt window there and run this program – to see the result of the assignment operations

![](img/d06b1f1cf83677f6647237f0c7827141_41_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_41_1.png)

Unlike the = assign operator, the == equality operator compares operands and is described here.

## Comparing values

The operators that are commonly used in Python programming to compare two operand values are listed in the table below:

| Operator: | Comparative test: |
| --- | --- |
| == | Equality |
| != | Inequality |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal to |
| <= | Less than or equal to |

The `==` equality operator compares two operands and will return `True` if both are equal in value, otherwise it will return a `False` value. If both are the same number they are equal, or if both are characters their ASCII code values are compared numerically to achieve the comparison result.

Conversely, the `!=` inequality operator returns `True` if two operands are not equal, using the same rules as the `==` equality operator, otherwise it returns `False`. Equality and inequality operators are useful in testing the state of two variables to perform conditional branching in a program according to the result.

![](img/d06b1f1cf83677f6647237f0c7827141_42_0.png)

A-Z uppercase characters have ASCII code values 65-90 and a-z lowercase characters have ASCII code values 97-122.

The ">" greater than " operator compares two operands and will return `True` if the first is greater in value than the second, or it will return `False` if it is equal or less in value. The "<" less than " operator makes the same comparison but returns `True` if the first operand is less in value than the second, otherwise it returns `False`. A ">" greater than " or <" less than " operator is often used to test the value of an iteration counter in a loop.

Adding the = operator after a > “greater than” or < “less than” operator makes it also return **True** if the two operands are exactly equal in value.

- Start a new Python script by initializing five variables with values for comparison

```python
nil = 0
num = 0
max = 1
cap = 'A'
low = 'a'
```

![](img/d06b1f1cf83677f6647237f0c7827141_43_0.png)

- Next, add statements to display the results of numeric and character equality comparisons

```python
print( 'Equality \t', nil, '==', num, nil == num )
print( 'Equality \t', cap, '==', low, cap == low )
```

- Now, add a statement to display the result of an inequality comparison

```python
print( 'Inequality \t', nil, '!=', max, nil != max )
```

- Then, add statements to display the results of greater and lesser comparisons

```python
print( 'Greater \t', nil, '>', max, nil > max )
print( 'Lesser \t', nil, '<', max, nil < max )
```

- Finally, add statements to display the results of greater or equal and lesser or equal comparisons

```python
print( 'More Or Equal \t', nil, '>=', num, nil >= num )
print( 'Less or Equal \t', max, '<=', num, max <= num )
```

- Save the file in your scripts directory, then open a Command Prompt window there and run this program – to see the result of comparison operations

```
Command Prompt
C:\MyScripts>python arithmetic.py
Addition:		8 + 2 = 10
Subtraction:	8 - 2 = 6
Multiplication:	8 × 2 = 16
Division:		8 ÷ 2 = 4.0
Floor Division:	8 ÷ 2 = 4
Modulus:		8 % 2 = 0
Exponent:		8**2 = 64
C:\MyScripts>■
```

![](img/d06b1f1cf83677f6647237f0c7827141_44_0.png)

The \t escape sequence shown here adds an invisible tab character to format the output.

![](img/d06b1f1cf83677f6647237f0c7827141_44_1.png)

The ASCII code value for uppercase “A” is 65, but for lowercase “a” it’s 97 – so their comparison here returns False.

## Assessing logic

The logical operators most commonly used in Python programming are listed in the table below:

| Operator: | Operation: |
| :-- | :-- |
| and | Logical AND |
| or | Logical OR |
| not | Logical NOT |

The logical operators are used with operands that have Boolean values of **True** or **False**, or are values that convert to **True** or **False**.

The (logical AND) **and** operator will evaluate two operands and return **True** only if both operands themselves are **True**. Otherwise the **and** operator will return **False**. This is used in conditional branching where the direction of a program is determined by testing two conditions – if both conditions are satisfied, the program will go in a certain direction, otherwise it will take a different direction.

Unlike the **and** operator that needs both operands to be **True**, the (logical OR) **or** operator will evaluate its two operands and return **True** if either one of the operands itself returns **True**. If neither operand returns **True**, then the **or** operator will return **False**. This is useful in Python programming to perform a certain action if either one of two test conditions has been met.

The (logical NOT) **not** operator is a unary operator that is used before a single operand. It returns the inverse value of the given operand, so if the variable a had a value of **True** then **not a** would have a value of **False**. The **not** operator is useful in Python programs to toggle the value of a variable in successive loop iterations with a statement like a = not a. This ensures that on each iteration of the loop, the Boolean value is reversed, like flicking a light switch on and off.
