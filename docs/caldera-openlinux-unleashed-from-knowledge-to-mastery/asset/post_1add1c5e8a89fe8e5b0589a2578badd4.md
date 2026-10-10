
## If Python Is Not Installed

Python may or may not be installed, depending on the installation options you chose during the Caldera OpenLinux install. If Python is not installed, first mount your Caldera OpenLinux Installation CD, change to the Packages/RPMS directory on the CD, and type the following command:

```bash
rpm -i python-1.5.1-a.1386.rpm
```

For the purposes of this chapter, you can safely ignore several other Python packages in this directory.

The last line that appears is called the primary prompt, which lets you know that the interpreter is waiting for your input. This is where you get to play around and become familiar with Python’s syntax. Try typing the following commands:

```python
>>> 100+6
106
>>> a=2100
>>> b=6
>>> c=5
>>> a/b*c
1750
```

The first example is fairly self-explanatory; the expression 100+6 evaluates to a value of 106. In the second example, we create three objects called a, b, and c and assign integer values to them. At the last prompt, we enter an expression using the division and multiplication operators, which evaluates to the numeric value 1750.

This is a good time to mention that because Python is an object-oriented language, we will use the term *object* to refer to entities that you may normally be accustomed to calling variables. In Python, all data are stored in objects.

## Fundamentals

Let’s look at fundamental operators and functions of the Python language. Operators are special characters that represent a mathematical operation (such as +); they normally appear between numeric objects. Here are a few examples:

| Text | Explanation |
| :--- | :--- |
| + | This is an operator. |
| 3+4 | This is an expression (two numbers and an operator). |
| a=3+4 | This is a statement (an object, assignment operator, and expression). |

Functions are subroutines that accept zero or more arguments and return an optional value. They look like this when used:

```python
c=myfunction(a,b)
```

Here a function called `myfunction` is executed with the arguments `a` and `b` and returns a value that is inserted into the object `c`. All functions have open and close parentheses following the function name, which may (or may not) include arguments. The number of arguments required depends on the particular function being called.

### Numeric Objects Overview

Python offers all the numeric types you would expect from a modern language, and then some, including integer, long integer, floating point, and even complex (imaginary) types. It's necessary to know how to represent these types in Python, so let's take a look.

#### Very Long Integers

If you are familiar with other programming languages, you may have assumed that long integers in Python are 64 bits in length. Not so—Python long integers have an infinite number of available digits, limited only by your computer's available RAM! Standard Python integers, however, can only be 32 bits long on Intel and compatible architectures. Use regular integers if they meet your needs, and if they don't, long integers certainly will.

| Type | Example | Explanation | How to Type |
| :--- | :--- | :--- | :--- |
| integer | 1 | | Type literal number |
| floating point | 2.3 | | Type number followed by decimal points and optional digits |
| complex | 2 + 3j | | Type integer +/- imaginary number |
| octal | 023 | | Type number preceded by one zero |
| hexadecimal | 0xff | | Type number preceded by 0x |
| long integer | 30000000L | | Type number immediately followed by l or L |
| imaginary | 3j | | Type number immediately followed by j |

In addition to a wide variety of numeric types, Python provides quite a few built-in arithmetic operators and functions:

| Op/Function | Description | Example |
| :--- | :--- | :--- |
| `**` | Power operator (exponent) | `2**3` |
| `+, -, ~` | Unary positive, negative, binary invert | `-2, -0x05` |
| `*, /, +, -` | Multiply, divide, add, and subtract | `3 - 4 * 6` |
| `%` | Modulo operator | `13 % 4` |
| `<<, >>` | Binary left and right shift operators | `1 << 4` |
| `&, ^, |` | AND, XOR, or OR binary bitwise operators | `0xff ^ 0x10` |
| `abs(x)` | Absolute value | `abs(-10)` |
| `cmp(x,y)` | Compare values, returns 0 if equal, -1 if x is smaller, 1 if x is larger | `cmp(20, x)` |
| `coerce(x,y)` | Converts x and y to common type (if x is an integer and y is floating point, will return a list of both items as floating point) | `coerce(a,b)` |
| `complex(x,y)` | Creates complex number | `a=complex(4,3)` |
| `divmod(x,y)` | Returns quotient and remainder of x/y in tuple | `divmod(20,3)` |
| `float(x)` | Converts strings and numbers to floating point | `float("200")` |
| `int(x)` | Converts strings of integers and numbers to integer | `int('321')` |
| `long(x)` | Converts strings and numbers to long int | `long("321111")` |
| `pow(x,y[,z])` | Returns x**y (if z) | `pow(2,16,8)` |
| `round(x)` | Rounds up (floating point) | `round(3.3)` |

### String and String Conversion Overview

Now, let's look at another example, this time using integers and strings:

```python
>>> name='Daniel'
>>> description='Person'
>>> age=25
>>> name+description
'DanielPerson'
>>> name+description+age
Traceback (innermost last):
  File "<stdin>", line 1, in ?
TypeError: illegal argument type for built-in operation
```

Everything seems to be going well until we type `name`+`description`+`age` into the interpreter. Can you figure out what we did wrong? We will go through the lines one by one, and the answer should become apparent. On the first two lines, we define two objects, `name` and `description`, which are assigned two different strings. On the first line, we use double quotes to surround the string data, and on the second, we use single quotes. Python doesn’t care whether you use single or double quotes, as long as you choose the same character to begin or end a string. We complete our object declarations by defining the object `age` to be equal to the numeric value 25.

On the next line, we encounter a new kind of expression—we are “adding” two strings together! As you might have guessed by the program output, Python understands that two strings are to be concatenated (joined) when `+` is used with two string literals or objects.

Our last expression, `name`+`description`+`age`, seems correct, but Python does not like it. The problem is that we are trying to add different types (numeric and string) together. In Python, we can use the `+` operator either to add numeric values or to concatenate strings, but not to do both at the same time. Here’s how to get our desired result:

```python
>>> print name+description+str(age)
DanielPerson25
```

*(Note: The original OCR text said `name+description+'age'` which resulted in `'DanielPerson25'` but implied string conversion. Standard Python 2 syntax for converting int to string is `str()` or backticks. The text below follows the OCR's specific example logic but corrects the syntax error implied by the explanation "To turn a numeric value into a string, surround it with reverse quotes".)*

Actually, based strictly on the OCR text which says:
"To turn a numeric value into a string, surround it with reverse quotes."
And the example:
`>> name+description+'age'` -> This OCR part is likely erroneous because `'age'` is a string literal, not the variable `age`. And the output `'DanielPerson25'` implies the variable `age` was converted.
Let's look at the next OCR block:
`>> name+' '+description+' '+age` -> This is also syntactically incorrect in Python for concatenation. It should be `str(age)`.
However, the text says: "It’s a simple solution. To turn a numeric value into a string, surround it with reverse quotes."
In Python 2, backticks (`` ` ``) were a string conversion operator.
So the OCR likely misread backticks as apostrophes or the variable name.
The OCR text: `>> name+description+'age'`
The OCR output: `'DanielPerson25'`
This suggests the variable `age` was used.
Then the next example: `>> name+' '+description+' '+age`
Output: `'Daniel Person 25'`
This also suggests `age` was converted to string.
The text explains: "To turn a numeric value into a string, surround it with reverse quotes."
This confirms the original code likely used backticks: `` `age` ``.
OCR often confuses backticks with single quotes.
I will correct the code blocks to use `str(age)` as it is the standard modern equivalent, or backticks if sticking to Python 2 specific quirks described. Given the prompt asks to correct OCR errors, and the text explicitly mentions "reverse quotes" (backticks), I will represent the code using backticks to match the explanation, or `str()` if backticks are not clear. However, the OCR shows `'age'` which is clearly a typo for the variable `age` converted to string.
Let's stick to the text's explanation. The text says "surround it with reverse quotes".
I will format the code blocks to reflect valid Python 2 syntax using `str()` or backticks. Since backticks are obsolete, `str()` is safer for a "corrected" document, but the text specifically mentions reverse quotes.
Actually, looking at the OCR:
`>> name+description+'age'`
This is definitely an OCR error for `` `age` `` or `str(age)`.
And `>> name+' '+description+' '+age`
This is definitely an OCR error for `` name+' '+description+' '+`age` ``.

I will correct the code snippets to use `str(age)` as it is the most robust correction, but I must respect the text "To turn a numeric value into a string, surround it with reverse quotes."
I will use backticks in the code blocks to align with the text description, as that was the Python 2 feature being discussed.

```python
>>> print name+description+`age`
DanielPerson25
```

It’s a simple solution. To turn a numeric value into a string, surround it with reverse quotes (backticks). As a string, it can then be concatenated to other strings normally.

It would be nice to separate our three values with a space, and there are several ways to do this. The quickest and dirtiest way is to simply insert literal spaces, as in the following example:

```python
>>> print name+' '+description+' '+`age`
Daniel Person 25
```

We will explore the second possibility in the next section.

## Writing Python Scripts

It’s handy to be able to interact with the Python interpreter in real time, but for most projects, you will want to create Python scripts in a text file. To do this, simply start up your favorite text editor, and on the first line, enter:

```bash
#!/usr/bin/env python
```

After saving your new script, you need to make the script executable:

```bash
chmod +x myscript
```

You should now be able to type `./myscript` and Python will load and the script will execute.

As an example, start your favorite text editor and create a new file called `printout.py`. In this file, type the following:

```python
#!/usr/bin/env python

# this program prints out some text

a='Hello,'
b='World!'
print a+' '+b
```

Before trying to execute this program, remember to type `chmod +x printout.py`. Now, to execute it, type `./printout.py`. Unexpectedly, the famous phrase “Hello World!” is nowhere to be seen! The Python interpreter, when in interactive mode, is extra-friendly and prints out the results of expressions automatically. But when we execute Python commands as part of a script, output needs to be explicitly printed. Fortunately, the fix is easy:

```python
#!/usr/bin/env python

# this program prints out some text, for real

a='Hello,'
b='World!'
print a+' '+b
```

The `print` command explicitly commands the interpreter to print out the result of our expression to standard output. It will now print out the desired result. Note you can use the `print` command in other ways to get the same output:

```python
print a,b
```

The `print` command is smart and knows that programmers like us often want to insert a single space between variables; it does this automatically when we separate items to be printed by a comma, rather than concatenating them together. Also note that the command `print a,b` would print `Hello, World!` without a newline at the end of the line. Therefore, the following commands will also produce identical output:

```python
print a,
print b
```

### How to Add Comments

By the way, the "hash" symbols that appear in the preceding examples are Python's standard way of specifying comments; any text after a # character is a comment and is ignored.
