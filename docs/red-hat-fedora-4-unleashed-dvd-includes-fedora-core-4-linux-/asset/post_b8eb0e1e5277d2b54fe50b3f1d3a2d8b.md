
When you are done, press **Ctrl+D** to exit. At this point, all your variables and commands are forgotten by the interpreter, which is why complex Python programs are always saved in scripts!

## The Basics of Python

Python is a language wholly unlike most others, and yet it is so logical that most people can pick it up very quickly. You have already seen how easily you can assign strings, but in Python nearly everything is that easy—as long as you remember the syntax!

### Numbers

The way Python handles numbers is fairly standard, although it is more precise than some other languages. It has all the normal operators—such as **+** for addition, **-** for subtraction, **/** for division, and **\*** for multiplication—but it adds **%** for modulus (division remainder), **\*\*** for raise to the power, and **//** for floor division. It is also very specific about which type of number is being used, as this example shows:

```python
>>> a = 5
>>> b = 10
>>> a * b
50
>>> a / b
0
>>> b = 10.0
>>> a / b
0.5
>>> a // b
0.0
```

The first division returns **0** because both **a** and **b** are integers (whole numbers), so Python calculates the division as an integer, giving **0**. By converting **b** to **10.0**, Python considers it to be a floating-point number and so the division is now calculated as a floating-point value, giving **0.5**. Even with **b** being floating-point, using **//**—floor division—rounds it down.

Using **\*\***, you can easily see how Python works with integers:

```python
>>> 2 ** 30
1073741824
>>> 2 ** 31
2147483648L
```

The first statement raises **2** to the power of **30** (that is, $2 \times 2 \times 2 \times 2 \times 2 \times ...$), and the second raises **2** to the power of **31**. Notice how the second number has a capital **L** on the end of it—this is Python telling you that it is a long integer. The difference between long integers and normal integers is slight but important: Normal integers can be calculated using simple instructions on the CPU, whereas long integers—because they can be as big as you need them to be—need to be calculated in software and therefore are slower.

When specifying big numbers, you need not put the L at the end—Python will figure it out for you. Furthermore, if a number starts off as a normal number and then exceeds its boundaries, Python automatically converts it to a long integer. The same is not true the other way around: If you have a long integer and then divide it by another number so that it could be stored as a normal integer, it remains a long integer:

```python
>>> num = 99999999999999999999999999999999999L
>>> num = num / 1000000000000000000000000000000
>>> num
999L
```

You can convert between number types using typecasting, like this:

```python
>>> num = 10
>>> int(num)
10
>>> float(num)
10.0
>>> long(num)
10L
>>> floatnum = 10.0
>>> int(floatnum)
10
>>> float(floatnum)
10.0
>>> long(floatnum)
10L
```

You need not worry whether you are using integers or long integers; Python handles it all for you, so you can concentrate on getting the code right.

### More on Strings

Python stores strings as an immutable sequence of characters—a jargon-filled way of saying “it is a collection of characters that, once set, cannot be changed without creating a new string.” Sequences are important in Python. There are three primary types, of which strings are one, and they share some properties. Mutability makes much sense when you learn about lists in the next section.

As you saw in the previous example, you can assign a value to strings in Python with just an equal sign, like this:

```python
>>> mystring = 'hello';
>>> myotherstring = "goodbye";
>>> mystring
'hello'
>>> myotherstring;
'goodbye'
>>> test = "Are you really Bill O'Reilly?"
>>> test
"Are you really Bill O'Reilly?"
```

The first example encapsulates the string in single quotation marks and the second and third in double quotation marks. However, printing the first and second strings show them both in single quotation marks because Python does not distinguish between the two. The third example is the exception—it uses double quotation marks because the string itself contains a single quotation mark. Here, Python prints the string with double quotation marks because it knows it contains the single quotation mark.

Because the characters in a string are stored in sequence, you can index into them by specifying the character you are interested in. Like most other languages, these indexes are zero-based, which means you need to ask for character 0 to get the first letter in a string. For example:

```python
>>> string = "This is a test string"
>>> string
'This is a test string'
>>> string[0]
'T'
>>> string [0], string[3], string [20]
('T', 's', 'g')
```

The last line shows how, with commas, you can ask for several indexes at the same time. You could print the entire first word using this:

```python
>>> string[0], string[1], string[2], string[3]
('T', 'h', 'i', 's')
```

However, for that purpose you can use a different concept: slicing. A slice of a sequence draws a selection of indexes. For example, you can pull out the first word like this:

```python
>>> string[0:4]
'This'
```

The syntax there means “take everything from position 0 (including 0) and end at position 4 (excluding it).” So, [0:4] copies the items at indexes 0, 1, 2, and 3. You can omit either side of the indexes, and it will copy either from the start or to the end:

```python
>>> string [:4]
'This'
>>> string [5:]
'is a test string'
>>> string [11:]
'est string'
```

You can also omit both numbers, and it will give you the entire sequence:

```python
>>> string [:]
'This is a test string'
```

Later you will learn precisely why you would want to do that, but for now there are a number of other string intrinsics that will make your life easier. For example, you can use the + and * operators to concatenate (join) and repeat strings, like this:

```python
>>> mystring = "Python"
>>> mystring * 4
'PythonPythonPythonPython'
>>> mystring = mystring + " rocks! "
>>> mystring * 2
'Python rocks! Python rocks! '
```

In addition to working with operators, Python strings come with a selection of built-in methods. You can change the case of the letters with capitalize() (uppercases the first letter and lowercases the rest), lower() (lowercases them all), title() (uppercases the first letter in each word), and upper() (uppercases them all). You can also check whether strings match certain cases with islower(), istitle(), and isupper(); that also extends to isalnum() (returns true if the string is letters and numbers only) and isdigit() (returns true if the string is all numbers).

This example demonstrates some of these in action:

```python
>>> string
'This is a test string'
>>> string.upper()
'THIS IS A TEST STRING'
>>> string.lower()
'this is a test string'
>>> string.isalnum()
False
>>> string = string.title()
>>> string
'This Is A Test String'
```

Why did isalnum() return false—our string contains only alphanumeric characters, doesn't it? Well, no. There are spaces in there, which is what is causing the problem. More importantly, we were calling upper() and lower() and they were not changing the contents of the string—they just returned the new value. So, to change our string from This is a test string to This is A Test String, we actually have to assign it back to the string variable.

## Lists

Python’s built-in list data type is a sequence, like strings. However, they are mutable, which means they can be changed. Lists are like arrays in that they hold a selection of elements in a given order. You can cycle through them, index into them, and slice them:

```python
>>> mylist = ["python", "perl", "php"]
>>> mylist
['python', 'perl', 'php']
>>> mylist + ["java"]
['python', 'perl', 'php', 'java']
>>> mylist * 2
['python', 'perl', 'php', 'python', 'perl', 'php']
>>> mylist[1]
'perl'
>>> mylist[1] = "c++"
>>> mylist[1]
'c++'
>>> mylist[1:3]
[ 'c++', 'php']
```

The brackets notation is important: You cannot use parentheses, (( and )) or braces (\{ and \}) for lists. Using * for lists is different from using + for numbers. Python detects you are working with a list and appends one list to another. This is known as operator overloading, and it is one of the reasons Python is so flexible.

Lists can be nested, which means you can put a list inside a list. However, this is where mutability starts to matter, and so this might sound complicated! If you recall, the definition of an immutable string sequence is that it is a collection of characters that, once set, cannot be changed without creating a new string. Lists are mutable as opposed to immutable, which means you can change your list without creating a new list.

This becomes important because Python, by default, copies only a reference to a variable rather than the full variable. For example:

```python
>>> list1 = [1, 2, 3]
>>> list2 = [4, list1, 6]
>>> list1
[1, 2, 3]
>>> list2
[4, [1, 2, 3], 6]
```

Here we have a nested list. list2 contains 4, then list1, then 6. When you print the value of list2, you can see it also contains list1. Now, proceeding on from that:
