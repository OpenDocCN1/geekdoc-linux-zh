2. What are the \n characters shown on line 4 of Example 16.8?

3. What happens if you edit the file somedata.txt, and enter the numbers 23, 33, 43, and 54 on a single line in your text editor instead of on four different lines, save the file, and try to perform the same action in Example 16.8 in Python on the new file somedata.txt?

4. After you close the file, can you still access the values 43 and 54 in any way?

5. How would you specify the third element of the list x1?

# 16.3.7 Lists and the List Function

On the lowest level of the organizational scheme for Python, the list is an object that can contain multiple elements of possibly different types. Just like a shopping list can contain different kinds of things from a store, such as food, household goods, automotive supplies, and so on, a Python list can be made up of different types of elements, like integers, real numbers, strings, and so on; in fact, any type of Python object. For example:

```
>>>A = [ 34, 'Bob', 54.76, [4,7,9]]
```

is an expression that assigns the integer 34, the string "Bob", the real number 54.76, and another list comprised of the numbers 4, 7, and 9 to a variable named A. List indices are integers, starting with 0. So, the following statements in Python yield the results:

```
>>>A[2]
54.76
>>>A[0]
34
>>>A[3][2]
9
```

A 2×2 matrix (or array) can be specified as:

```
B = [[x1, x2], [y1, y2]]
```

Here is Python code that works on objects (please notice that your results will differ from the output shown here, since the numbers shown in the example are randomly generated):

# Example 16.10

```
>>> import random # random is a function from the Standard Library
>>> x = list(list (random.random() for i in range(3)) for j in range(3))
>>> x
```