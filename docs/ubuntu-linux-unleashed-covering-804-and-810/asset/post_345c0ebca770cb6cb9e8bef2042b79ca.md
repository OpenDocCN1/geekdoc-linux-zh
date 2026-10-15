
['graham', 'julian', 'nick', 'paul']
>>> list5.pop()
'paul'
>>> list5
['graham', 'julian', 'nick']
>>> list5.append('Rebecca')

In addition, one interesting method of strings returns a list: split(). This takes a character to split by and then gives you a list in which each element is a chunk from the string. For example:

```
>>> string = "This is a test string";
>>> string.split(' ')
['This', 'is', 'a', 'test', 'string']
```

Lists are used extensively in Python, although this is slowly changing as the language matures.

## Dictionaries

Unlike lists, dictionaries are collections with no fixed order. Instead, they have a key (the name of the element) and a value (the content of the element), and Python places them wherever it needs to for maximum performance. When defining dictionaries, you need to use braces ({ }) and colons (:). You start with an opening brace and then give each element a key and a value, separated by a colon, like this:

```
>>> mydict = { 'perl': 'a language', 'php': 'another language' }
>>> mydict
{'php': 'another language', 'perl': 'a language'}
```

This example has two elements, with keys perl and php. However, when the dictionary is printed, we find that php comes before perl—Python hasn't respected the order in which we entered them. We can index into a dictionary using the normal code:

```
>>> mydict["perl"]
'a language'
```

However, because a dictionary has no fixed sequence, we cannot take a slice, or index by position.

Like lists, dictionaries are mutable and can also be nested; however, unlike lists, you cannot merge two dictionaries by using +. This is because dictionary elements are located using the key. Therefore, having two elements with the same key would cause a clash. Instead, you should use the update() method, which merges two arrays by overwriting clashing keys.

You can also use the keys() method to return a list of all the keys in a dictionary.

## Conditionals and Looping

So far, we have just been looking at data types, which should show you how powerful Python's data types are. However, you simply cannot write complex programs without conditional statements and loops.

Python has most of the standard conditional checks, such as, > (greater than), <= (less than or equal to), and == (equal), but it also adds some new ones, such as in. For example, we can use in to check whether a string or a list contains a given character/element:

```
>>> mystring = "J Random Hacker"
>>> "r" in mystring
True
>>> "Hacker" in mystring
True
>>> "hacker" in mystring
False
```

The last example demonstrates how in is case sensitive. We can use the operator for lists, too:

```
>>> mylist = ["soldier", "sailor", "tinker", "spy"]
>>> "tailor" in mylist
False
```

Other comparisons on these complex data types are done item by item:

```
>>> list1 = ["alpha", "beta", "gamma"]
>>> list2 = ["alpha", "beta", "delta"]
>>> list1 > list2
True
```

list1's first element (alpha) is compared against list2's first element (alpha) and, because they are equal, the next element is checked. That is equal also, so the third element is checked, which is different. The γ in gamma comes after the δ in delta in the alphabet, so gamma is considered greater than delta and list1 is considered greater than list2.

Loops come in two types, and both are equally flexible. For example, the for loop can iterate through letters in a string or elements in a list:

```
>>> string = "Hello, Python!"
>>> for s in string: print s,
...
H e l l o ,   P y t h o n !
```

The for loop takes each letter in string and assigns it to s. This then is printed to the screen using the print command, but note the comma at the end; this tells Python not to insert a line break after each letter. The "..." is there because Python allows you to enter more code in the loop; you need to press Enter again here to have the loop execute.

The exact same construct can be used for lists:

```
>>> mylist = ["andi", "rasmus", "zeeV"]
>>> for p in mylist: print p
...
andi
rasmus
zeeV
```

Without the comma after the print statement, each item is printed on its own line.

The other loop type is the while loop, and it looks similar:

```
>> while 1: print "This will loop forever!"
...
This will loop forever!
This will loop forever!
This will loop forever!
This will loop forever!
This will loop forever!
(etc)
Traceback (most recent call last):
  File "<stdin>", line 1, in ?
KeyboardInterrupt
>>>
```

That is an infinite loop (it will carry on printing that text forever), so you need to press Ctrl+C to interrupt it and regain control.

If you want to use multiline loops, you need to get ready to use your Tab key: Python handles loop blocks by recording the level of indent used. Some people find this odious; others admire it for forcing clean coding on users. Most of us, though, just get on with programming!

For example:

```
>>> i = 0
>>> while i < 3:
...     j = 0
...     while j < 3:
...         print "Pos: (" + str(i) + "," + str(j) + ")"
...         j += 1
...     i += 1
...
Pos: (0,0)
Pos: (0,1)
Pos: (0,2)
Pos: (1,0)
```
