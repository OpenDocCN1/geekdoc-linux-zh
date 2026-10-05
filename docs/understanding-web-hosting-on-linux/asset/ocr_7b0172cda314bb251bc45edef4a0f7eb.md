```
// declare a variable named x as type integer
int x;

// declare variable named ch as character variable
char ch;

// declare an integer variable named y and initialize it to 1
int y = 1;

// declare a character variable named ch and initialize it to A
char ch = 'A';
```

Figure 7.3: Variables can be declared and initialized with the same statement

# # Arithmetic Operators

The arithmetic operators for addition, subtraction, multiplication, and division are +, -, *, and /. Here are two examples of statements that use these arithmetic operators:

```
linetotal = (qty * price) - discount;
percent = amounttotal + amount;
```

The mod (remainder) operation is also supported, through the % character. For example, the following statement will assign the value of two to variable x:

```
x = 12 % 5;
```

There is no symbol for exponentiation. You must use the Java pow method of the math class (Math.pow). You will see an example of this in the sample mortgage program later in this chapter.

# # Unary Operators

There are four unary operators in Java: - (negation), ++ (increment), -- (decrement), and ~ (bitwise complement). The negation operator is simple. If you want to negate a value, you simply precede it with the negation character.

The increment and decrement operators can be used in two different ways. The first is pre-increment or -decrement, like this:

```
int counter = 1;
int totalcounter = ++counter; // totalcounter equals 2
```

Because the unary ++ operator precedes the counter, it is incremented before the value is assigned to totalcounter. If counter was equal to one prior to this operation, totalcounter equals two.

You can post-increment a variable by following the variable with the unary ++ operator:

```
int counter = 1;
int totalcounter = counter++; // totalcounter equals 1
```