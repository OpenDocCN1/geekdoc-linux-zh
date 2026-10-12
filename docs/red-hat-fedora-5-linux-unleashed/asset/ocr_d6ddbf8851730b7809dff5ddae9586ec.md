The for loop takes each letter in string and assigns it to s. The letter is then printed to the screen using the print command, but note the comma at the end; this tells Python not to insert a line break after each letter. The "..." is there because Python allows you to enter more code in the loop; you need to press Enter again here to have the loop execute.

The same construct can be used for lists:

```
```
>>> mylist = ["andi", "rasmus", "zeev"]
>>> for p in mylist: print p
...
andi
rasmus
zeev
```
```

Without the comma after the print statement, each item is printed on its own line.

The other loop type is the while loop, and it looks similar:

```
```
>>> while 1: print "This will loop forever!"
...
This will loop forever!
This will loop forever!
This will loop forever!
This will loop forever!
This will loop forever!
This will loop forever!
(etcs)
Traceback (most recent call last):
  File "<stdin>", line 1, in ?
KeyboardInterrupt
>>>
```
```

That is an infinite loop (it will carry on printing that text forever), so you have to press Ctrl+C to interrupt it and regain control.

If you want to use multiline loops, you need to get ready to use your Tab key: Python handles loop blocks by recording the level of indent used. Some people find this odious; others admire it for forcing clean coding on users. Most of us, though, just get on with programming!

For example:

```
```
>>> i = 0
>>> while i < 3:
...     j = 0
...     while j < 3:
...         print "Pos: " + str(i) + ", " + str(j) + "\"
...     j += 1
...
...     i += 1
... 
```
```