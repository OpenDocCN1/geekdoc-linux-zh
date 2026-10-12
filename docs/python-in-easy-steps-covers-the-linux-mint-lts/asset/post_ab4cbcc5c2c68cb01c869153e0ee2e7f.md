
## Casting data types

Although Python variables can store data of any data type, it is important to recognize the different types of data they contain to avoid errors when manipulating that data in a program. There are several Python data types but by far the most common ones are `str` (string), `int` (integer), and `float` (floating-point).

Data type recognition is especially important when assigning numeric data to variables from user input as it is stored by default as a `str` (string) data type. String values cannot be used for arithmetical expressions as attempting to add string values together simply concatenates (joins) the values together rather than adding them numerically. For example `'8' + '4' = '84'`.

Fortunately, the data type of stored values can be easily converted (“cast”) into a different data type using built-in Python functions. The value to be converted is specified within the parentheses that follow the function name. Casting `str` (string) values to become `int` (integer) values allows them to be used for arithmetical expressions, for example, `8 + 4 = 12`.

Python’s built-in data type conversion functions return a new object representing the converted value, and those conversion functions most frequently used are listed in the table below:

| Function | Description |
| :--- | :--- |
| `int(x)` | Converts x to an integer whole number |
| `float(x)` | Converts x to a floating-point number |
| `str(x)` | Converts x to a string representation |
| `chr(x)` | Converts integer x to a character |
| `unichr(x)` | Converts integer x to a Unicode character |
| `ord(x)` | Converts character x to its integer value |
| `hex(x)` | Converts integer x to a hexadecimal string |
| `oct(x)` | Converts integer x to an octal string |

The Python built-in `type()` function can be used to determine to which data type class the value contained in a variable belongs, simply by specifying that variable’s name within its parentheses.

![](img/d06b1f1cf83677f6647237f0c7827141_55_0.png)

> Converting a **float** (floating-point) data type to an **int** (integer) data type will truncate the number at the decimal point losing the fraction.

1. Start a new Python script by initializing two variables with numeric values from user input

   ```python
   a = input( 'Enter A Number: ' )
   b = input( 'Now Enter Another Number: ' )
   ```

   ![](img/d06b1f1cf83677f6647237f0c7827141_55_1.png)

2. Next, add statements to add the variable values together then display the combined result and its data type – to see a concatenated string value result

   ```python
   sum = a + b
   print( '\nData Type sum :' , sum , type( sum ) )
   ```

3. Now, add statements to add cast variable values together then display the result and its data type – to see a total integer value result

   ```python
   sum = int( a ) + int( b )
   print( 'Data Type sum :' , sum , type( sum ) )
   ```

4. Then, add statements to cast a variable value then display the result and its data type – to see a total float value

   ```python
   sum = float( sum )
   print( 'Data Type sum :' , sum , type( sum ) )
   ```

5. Finally, add statements to cast an integer representation of a variable value then display the result and its data type – to see a character string value

   ```python
   sum = chr( int( sum ) )
   print('Data Type sum :',sum, type(sum) )
   ```

6. Save the file in your scripts directory, then open a Command Prompt window there and run this program – to see the result of casting as various data types

   ```bash
   Command Prompt
   C:\\MyScripts>python cast.py
   Enter A Number: 60
   Now Enter Another Number: 5
   Data Type sum : 605 <class 'str'>
   Data Type sum : 65 <class 'int'>
   Data Type sum : 65.0 <class 'float'>
   Data Type sum : A <class 'str'>
   C:\\MyScripts> 
   ```

   ![](img/d06b1f1cf83677f6647237f0c7827141_56_0.png)

The number 65 is the ASCII character code for uppercase letter A.

## Manipulating bits

In computer terms, each byte comprises eight bits that can each contain a 1 or a 0 to store a binary number, representing decimal values from 0 to 255. Each bit contributes a decimal component only when that bit contains a 1. Components are designated right-to-left from the “Least Significant Bit” (LSB) to the “Most Significant Bit” (MSB). The binary number in the bit pattern below is 00110010 and represents the decimal number 50 (2+16+32):

| Bit No. | 8 MSB | 7 | 6 | 5 | 4 | 3 | 2 | 1 LSB |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Decimal** | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| **Binary** | 0 | 0 | 1 | 1 | 0 | 0 | 1 | 0 |

![](img/d06b1f1cf83677f6647237f0c7827141_57_0.png)

Many Python programmers never use bitwise operators but it is useful to understand what they are and how they may be used.

It is possible to manipulate individual parts of a byte using the Python “bitwise” operators listed and described below:

| Operator | Name | Binary number operation |
| :--- | :--- | :--- |
| `\|` | OR | Return a 1 in each bit where either of two compared bits is a 1<br>Example: **1010 \| 0101 = 1111** |
| `&` | AND | Return a 1 in each bit where both of two compared bits is a 1<br>Example: **1010 & 1100 = 1000** |
| `~` | NOT | Return a 1 in each bit where neither of two compared bits is a 1<br>Example: **1010 ~ 0011 = 0100** |
| `^` | XOR | Return a 1 in each bit where only one of two compared bits is a 1<br>Example: **1010 ^ 0100 = 1110** |
| `<<` | Shift left | Move each bit that is a 1 a specified number of bits to the left<br>Example: **0010 << 2 = 1000** |
| `>>` | Shift right | Move each bit that is a 1 a specified number of bits to the right<br>Example: **1000 >> 2 = 0010** |

![](img/d06b1f1cf83677f6647237f0c7827141_58_0.png)

Each half of a byte is known as a “nibble” (4 bits). The binary numbers in the examples in the table describe values stored in a nibble.

Unless programming for a device with limited resources there is seldom a need to utilize bitwise operators, but they can be useful. For instance, the XOR (eXclusive OR) operator lets you exchange values between two variables without the need for a third variable.

![](img/d06b1f1cf83677f6647237f0c7827141_58_1.png)

### bitwise.py

1. Start a new Python script by initializing two variables with numeric values and display these initial values

   ```python
   a = 10
   b = 5
   print ('a =', a, 'b = ', b)
   ```

2. Next, add a statement to change the first variable’s decimal value by binary bit manipulation

   ```python
   # 1010 ^ 0101 = 1111 (decimal 15)
   a = a ^ b
   ```

3. Now, add a statement to change the second variable’s decimal value by binary bit manipulation

   ```python
   # 1111 ^ 0101 = 1010 (decimal 10)
   b = a ^ b
   ```

4. Then, add a statement to change the first variable’s decimal value once more by further bit manipulation

   ```python
   # 1111 ^ 1010 = 0101 (decimal 5)
   a = a ^ b
   ```

5. Finally, add a statement to display the exchanged values

   ```python
   print('a =', a, '\tb =', b)
   ```

6. Save the file in your scripts directory, then open a Command Prompt window there and run this program - to see the result of bitwise operations

   ```bash
   C:\MyScripts>python bitwise.py
   a = 10    b =     5
   a =  5    b =    10
   C:\MyScripts>
   ```

   ![](img/d06b1f1cf83677f6647237f0c7827141_59_0.png)

> Do not confuse bitwise operators with logical operators. Bitwise operators compare binary numbers, whereas logical operators evaluate Boolean values.

## Summary

- Arithmetical operators can form expressions with two operands for addition `+`, subtraction `-`, multiplication `*`, division `/`, floor division `//`, modulo `%`, or exponent `**`.

- The assignment `=` operator can be combined with an arithmetical operator to perform an arithmetical calculation then assign its result.

- Comparison operators can form expressions comparing two operands for equality `==`, inequality `!=`, greater `>`, lesser `<`, greater or equal `>=`, and lesser or equal `<=` values.

- Logical `and` and `or` operators form expressions evaluating two operands to return a Boolean value of `True` or `False`.

- The logical `not` operator returns the inverse Boolean value of a single operand.

- A conditional `if-else` expression evaluates a given expression for a Boolean `True` or `False` value, then returns one of two operands depending on its result.

- Expressions containing multiple operators will execute their operations in accordance with the default precedence rules unless explicitly determined by the addition of parentheses `()`.

- The data type of a variable value can be converted to a different data type by the built-in Python functions `int()`, `float()`, and `str()` to return a new converted object.

- Python’s built-in `type()` function determines to which data type class a specified variable belongs.

- Bitwise operators OR `|`, AND `&`, NOT `~`, and XOR `^` each return a value after comparison of the values within two bits, whereas the Shift left `<<` and Shift right `>>` operators move the bit values a specified number of bits in their direction.
