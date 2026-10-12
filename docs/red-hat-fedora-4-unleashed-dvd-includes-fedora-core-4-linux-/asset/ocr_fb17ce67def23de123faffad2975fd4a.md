# Conditionals and Looping

So far, we have just been looking at data types, which should show you how powerful Python’s data types are. However, you simply cannot write complex programs without conditional statements and loops.

Python has most of the standard conditional checks, such as `>` (greater than), `<=` (less than or equal to), and `==` (equal), but it also adds some new ones, such as `in`. For example, we can use `in` to check whether a string or a list contains a given character/element:

```
```text
>>> mystring = "J Random Hacker"
>>> "r" in mystring
True
>>> "Hacker" in mystring
True
>>> "hacker" in mystring
False
```
```

The last example demonstrates how `in` is case sensitive. We can use the operator for lists, too:

```
```text
>>> mylist = ["soldier", "sailor", "tinker", "spy"]
>>> "tailor" in mylist
False
```
```

Other comparisons on these complex data types are done item by item:

```
```text
>>> list1 = ["alpha", "beta", "gamma"]
>>> list2 = ["alpha", "beta", "delta"]
>>> list1 > list2
True
```
```

`list1`’s first element (alpha) is compared against `list2`’s first element (alpha) and, because they are equal, the next element is checked. That is equal also, so the third element is checked, which is different. The g in gamma comes after the d in delta in the alphabet, so gamma is considered greater than delta and `list1` is considered greater than `list2`.

Loops come in two types, and both are equally flexible. For example, the for loop can iterate through letters in a string or elements in a list:

```
```text
>>> string = "Hello, Python!"
>>> for s in string: print s,
...
Hello, Python!
```
```

The for loop takes each letter in string and assigns it to s. This then is printed to the screen using the print command, but note the comma at the end; this tells Python not