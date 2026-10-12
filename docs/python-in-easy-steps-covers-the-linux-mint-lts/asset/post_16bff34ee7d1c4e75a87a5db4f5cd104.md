
## message

```
C:\MyScripts>python hello.py
Hello world!

C:\MyScripts>
```

![](img/d06b1f1cf83677f6647237f0c7827141_22_0.png)

Don’t use a word processor to create program files as they add format information to the file.

![](img/d06b1f1cf83677f6647237f0c7827141_22_1.png)

The directory created at **C:\MyScripts** will be used to contain all Windows examples in this book.

The procedure to create the traditional first Python program is identical on Linux systems to that on Windows systems. It is, however, important to be aware, on any platform where different versions of Python are installed: you must use the correct command to call upon the particular Python interpreter required. This is especially important on Linux systems that often ship with the Python 2.7 version installed as their default. This means that the command `python` will assume you want to call that interpreter. Where Python 3.3 is installed, and you want to call that particular interpreter to process a script, you must use the command `python3.3` to explicitly call upon that version’s interpreter.

- 1. On Linux, launch any plain text editor such as the `Nano` application

![](img/d06b1f1cf83677f6647237f0c7827141_22_2.png)

- 2. Next, precisely type the following statement into the empty text editor window
  `print('Hello World!')`

- 3. Now, save the file in your home directory as **hello.py**

![](img/d06b1f1cf83677f6647237f0c7827141_23_0.png)

- 4. Finally, launch a Terminal window and navigate to your home directory and precisely enter the command `python3.3 hello.py` – to see the Python interpreter run your program and print out the specified greeting message

![](img/d06b1f1cf83677f6647237f0c7827141_23_1.png)

![](img/d06b1f1cf83677f6647237f0c7827141_23_2.png)

All further examples in this book are illustrated on Windows (simply because that platform has the most users) but they can also be created and executed on Linux.

## Employing variables

In programming, a “variable” is a container in which a data value can be stored within the computer’s memory. The stored value can then be referenced using the variable’s name. The programmer can choose any name for a variable, except the Python keywords listed on the inside front cover of this book, and it is good practice to choose meaningful names that reflect the variable’s content.

![](img/d06b1f1cf83677f6647237f0c7827141_24_0.png)

Data to be stored in a variable is assigned in a Python program declaration statement with the = assignment operator. For example, to store the numeric value eight in a variable named “a”:

```
a = 8
```

The stored value can then be referenced using the variable’s name, so that the statement print(a) will output the stored value 8. That variable can subsequently be assigned a different value, so its value can vary as the program proceeds – hence the term “variable”.

In Python programming, a variable must be assigned an initial value (“initialized”) in the statement that declares it in a program – otherwise the interpreter will report a “not defined” error.

Multiple variables can be initialized with a common value in a single statement using a sequence of = assignments. For example, to initialize variables named “a”, “b” and “c”, each with a numeric value of eight, like this:

```
a = b = c = 8
```

Alternatively, multiple variables can be initialized with differing values in a single statement using comma separators. For example, to initialize variables named “a”, “b” and “c” with numeric values of one, two and three respectively, like this:

```
a, b, c = 1, 2, 3
```

Some programming languages, such as Java, demand you specify what type of data a variable may contain in its declaration. This reserves a specific amount of memory space and is known as “static typing”. Python variables, on the other hand, have no such limitation and adjust the memory allocation to suit the various data values assigned to their variables (“dynamic typing”). This means they can store integer whole numbers, floating-point numbers, text strings, or Boolean values of **True** or **False** as required.

![](img/d06b1f1cf83677f6647237f0c7827141_25_0.png)

String data must be enclosed within quote marks to denote the start and end of the string.

![](img/d06b1f1cf83677f6647237f0c7827141_25_1.png)

Programming languages that require variable types to be specified are alternatively known as “strongly typed” whereas those that do not are alternatively known as “loosely typed”.

Optionally, comments can be added to your Python scripts to describe the purpose of statements or sections of code if preceded by a # hash character. Everything following the # hash character up to the end of the line is ignored by the Python interpreter. It is useful to comment your code to make its purpose clear to others or when revisiting the code yourself later.

- Launch a plain text editor, then declare and initialize a variable – then display its stored value
  ```
  # Initialize a variable with an integer value.
  var = 8
  print(var)
  ```

- 2. Next, assign a new value and display that stored value
  ```
  # Assign a float value to the variable.  
  var = 3.142  
  print(var)
  ```

- 3. Now, assign a different value and display the stored value
  ```
  # Assign a string value to the variable.  
  var = "Python in easy steps"  
  print(var)
  ```

- 4. Finally, assign another value and display the stored value
  ```
  # Assign a boolean value to the variable.  
  var = True  
  print(var)
  ```

- 5. Save the file in your scripts directory, then open a Command Prompt window there and run the program – to see the stored values output as the program proceeds

![](img/d06b1f1cf83677f6647237f0c7827141_26_1.png)

![](img/d06b1f1cf83677f6647237f0c7827141_26_2.png)

Multi-line comments can be added to a script if enclosed between triple quote marks “””, “”””.

## Obtaining user input

Just as a data value can be assigned to a variable in a Python script, a user-specified value can be assigned to a variable with the Python `input()` function. This accepts a string within its parentheses that will prompt the user for input by displaying that string then wait to read a line of input.

User input is read as a text string, even when it’s numeric, and can be assigned to a variable using the = assignment operator as usual. The value assigned to any variable can be displayed by specifying the variable name to the `print()` function – to reference that variable’s stored value.

Multiple values to be displayed can be specified to the `print()` function as a comma-separated list within its parentheses.

- 1. Launch a plain text editor, then declare and initialize a variable by requesting user input
  ```
  # Initialize a variable with a user-specified value.
  user = input( 'I am Python. What is your name? ' )
  ```

![](img/d06b1f1cf83677f6647237f0c7827141_27_0.png)

- 2. Next, display a response message confirming the input by referencing the stored user name
  ```
  # Output a string and a variable value.
  print('Welcome', user)
  ```

- 3. Now, save the file in your scripts directory then open a Command Prompt window there and run this program – enter your name, then hit Return to see the response message include your name

![](img/d06b1f1cf83677f6647237f0c7827141_28_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_28_1.png)

Notice that the prompt string ends with a space that is displayed in output — so the user entry is separated from the colon when typed in.

When multiple values are specified to the print() function it will display each value in output separated by a single space by default. An alternative separator can, however, be specified by adding a sep parameter to the comma-separated list. For example, `sep = '•'` will display each value in output separated by an asterisk character.

Output displayed by the print() function will, by default, add an invisible \n newline character at the end of the line to automatically move the print head to the next line. An alternative line ending can, however, be specified by adding an end parameter to the comma-separated list. For example, `end = '!'` will display each value in output then end the line with an exclamation mark.

- 4. Edit the script to declare and initialize a second variable by requesting more user input
  ```
  # Initialize another variable with a user-specified value.
  lang = input( 'Favorite programming language? : ' )
  ```

- 5. Next, display a response message confirming the input by referencing the stored language name — and specifying a custom separator and a custom line ending
  ```
  # Output a string and a variable value.
  print( lang , 'is', 'Fun' , sep = ' * ' , end = '!' )
  ```

- 6. Now, save the file once more, then open a Command Prompt window there and run this program again — enter your name and a programming
