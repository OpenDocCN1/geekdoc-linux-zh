using simple instructions on the CPU, whereas long integers—because they can be as big as you need them to be—need to be calculated in software and therefore are slower.

When specifying big numbers, you need not put the L at the end—Python will figure it out for you. Furthermore, if a number starts off as a normal number and then exceeds its boundaries, Python automatically converts it to a long integer. The same is not true the other way around: If you have a long integer and then divide it by another number so that it could be stored as a normal integer, it remains a long integer:

```
```python
>>> num = 99999999999999999999999999999999999L
>>> num = num / 1000000000000000000000000000000
>>> num
999L
```
```

You can convert between number types using typecasting, like this:

```
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
```

You need not worry whether you are using integers or long integers; Python handles it all for you, so you can concentrate on getting the code right.

# ## More on Strings

Python stores strings as an immutable sequence of characters—a jargon-filled way of saying “it is a collection of characters that, once set, cannot be changed without creating a new string.” Sequences are important in Python. There are three primary types, of which strings are one, and they share some properties. Mutability makes much sense when you learn about lists in the next section.

As you saw in the previous example, you can assign a value to strings in Python with just an equal sign, like this:

```
```python
>>> mystring = 'hello';
>>> myotherstring = "goodbye";
>>> mystring
```
```