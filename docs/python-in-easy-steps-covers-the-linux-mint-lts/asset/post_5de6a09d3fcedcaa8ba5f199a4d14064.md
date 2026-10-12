
```python
for item in zip(chars, fruit):
    print(item, end=' ')
```

5. Finally, add statements to display all dictionary key names and associated element values
   ```python
   print('\nPaired:')
   for key, value in dict.items():
       print(key, '=', value)
   ```
6. Save the file in your scripts directory, then open a Command Prompt window there and run this program – to see the items displayed by the loop iterations

![](img/d06b1f1cf83677f6647237f0c7827141_83_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_83_1.png)

In Python programming anything that contains multiple items that can be looped over is described as “iterable”.

## Breaking out of loops

The Python `break` keyword can be used to prematurely terminate a loop when a specified condition is met. The `break` statement is situated inside the loop statement block and is preceded by a test expression. When the test returns **True**, the loop ends immediately and the program proceeds on to the next task. For example, in a nested inner loop it proceeds to the next iteration of the outer loop.

1. Start a new Python script with a statement creating a loop that iterates three times
   `for i in range(1, 4):`

![](img/d06b1f1cf83677f6647237f0c7827141_84_0.png)

2. Next, add an indented statement creating a “nested” inner loop that also iterates three times
   `for j in range(1, 4):`

3. Now, add a further-indented statement in the inner loop to display the counter numbers (of both the outer loop and the inner loop) on each iteration of the inner loop
   `print('Running i=', i, ' j=', j)`

4. Save the file in your scripts directory, then open a Command Prompt window there and run this program – to see the counter values on each loop iteration

![](img/d06b1f1cf83677f6647237f0c7827141_85_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_85_1.png)

Compare these nested **for** loops with the nested **while** loops example here.

5. Now, insert this **break** statement at the very beginning of the inner loop block, to break out of the inner loop – then save the file and run the program once more

```python
if i == 2 and j == 1 :
    print('Breaks inner loop at i=2 j=1')
    break
```

![](img/d06b1f1cf83677f6647237f0c7827141_85_2.png)

![](img/d06b1f1cf83677f6647237f0c7827141_85_3.png)

The Python `continue` keyword can be used to skip a single iteration of a loop when a specified condition is met. The `continue` statement is situated inside the loop statement block and is preceded by a test expression. When the test returns **True**, that one iteration ends and the program proceeds to the next iteration.

6. Insert this `continue` statement at the beginning of the inner loop block, to skip the first iteration of the inner loop – then save the file and run the program again

```python
if i == 1 and j == 1 :
    print('Continues inner loop at i=1 j=1')
    continue
```

![](img/d06b1f1cf83677f6647237f0c7827141_86_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_86_1.png)

![](img/d06b1f1cf83677f6647237f0c7827141_86_2.png)

Here, the **break** statement halts all three iterations of the inner loop when the outer loop tries to run it the second time.

![](img/d06b1f1cf83677f6647237f0c7827141_86_3.png)

Here, the **continue** statement just skips the first iteration of the inner loop when the outer loop tries to run it for the first time.

## Summary

- In Python, multiple assignments can be used to initialize several variables in a single statement.
- A Python list is a variable that can store multiple items of data in sequentially-numbered elements that start at zero.
- Data stored in a list element can be referenced using the list name followed by an index number in [ ] square brackets.
- The `len()` function returns the length of a specified list.
- A Python tuple is an immutable list whose values can be assigned to individual variables by “sequence unpacking”.
- Data stored in a tuple element can be referenced using the tuple name followed by an index number in [ ] square brackets.
- A Python set is an unordered collection of unique elements whose values can be compared and manipulated by its methods.
- Data stored in a set cannot be referenced by index number.
- A Python dictionary is a list of key:value pairs of data in which each key must be unique.
- Data stored in a dictionary element can be referenced using the dictionary name followed by its key in [ ] square brackets.
- The Python `if` keyword performs a conditional test on an expression for a Boolean value of `True` or `False`.
- Conditional branching provides alternatives to an `if` test with the `else` and `elif` keywords.
- A `while` loop repeats until a test expression returns `False`.
- A `for in` loop iterates over each item in a specified list or string.
- The range() function generates a numerical sequence that can be used to specify the length of a for in loop.
- The break and continue keywords interrupt loop iterations.

# 4

## Defining functions

*This chapter demonstrates how to create functions that can be called to execute statements when the program requires them.*

- Understanding scope
- Supplying arguments
- Returning values
- Using callbacks
- Adding placeholders
- Producing generators
- Handling exceptions
- Debugging assertions
- Summary

### Understanding scope

Previous examples in this book have used built-in functions of the Python programming language, such as the `print`() function. However, most Python programs contain a number of custom functions that can be called as required when the program runs.

A custom function is created using the `def` (definition) keyword followed by a name of your choice and ( ) parentheses. The programmer can choose any name for a function except the Python keywords listed on the inside front cover of this book, and the name of an existing built-in function. This line must end with a `:` colon character, then the statements to be executed whenever the function gets called must appear on lines below and be indented. Syntax of a function definition, therefore, looks like this:

```python
def function-name():
    statements-to-be-executed
    statements-to-be-executed
```

Once the function statements have been executed, program flow resumes at the point directly following the function call. This modularity is very useful in Python programming to isolate set routines so they can be called upon repeatedly.

To create custom functions it is necessary to understand the accessibility (“scope”) of variables in a program:

- Variables created outside functions can be referenced by statements inside functions – they have “global” scope.
- Variables created inside functions cannot be referenced from outside the function in which they have been created – these have “local” scope.

The limited accessibility of local variables means that variables of the same name can appear in different functions without conflict.

If you want to coerce a local variable to make it accessible elsewhere, it must first be declared with the Python `global` keyword followed by its name only. It may subsequently be assigned a value that can be referenced from anywhere in the program. Where a global variable and a local variable have the same name, the function will use the local version.

![](img/d06b1f1cf83677f6647237f0c7827141_92_0.png)

Function statements must be indented from the definition line by the same amount so the Python interpreter can recognize the block.

![](img/d06b1f1cf83677f6647237f0c7827141_92_1.png)

Avoid using global variables in order to prevent accidental conflict – use only local variables where possible.

1. Start a new Python script by initializing a global variable
   `global_var = 1`

   ![](img/d06b1f1cf83677f6647237f0c7827141_92_2.png)

2. Next, create a function named "my_vars" to display the value contained within the global variable
   ```python
   def my_vars():
       print('Global Variable:', global_var)
   ```

3. Now, add indented statements to the function block to initialize a local variable and display the value it contains
   ```python
   local_var = 2
   print('Local variable:', local_var)
   ```

4. Then, add indented statements to the function block to create a coerced global variable and assign an initial value
   ```python
   global inner_var
   inner_var = 3
   ```
