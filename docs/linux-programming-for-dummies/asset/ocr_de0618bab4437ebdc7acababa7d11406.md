+   4. How you use can *pseudo-code* as comments for your program? (Yes, **this one is an essay question**)

**Answer**: you can list instructions that are necessary to complete a task as pseudo-code (that is, the instructions that you write in real English) in your program file. Linux, of course, doesn't understand English. You can, however, place a number sign (#) as the first character of the pseudo-code, which converts the pseudo-code into a comment.

# ## Chapter 19: Stamping Out Bugs in Your Program

+   1. What's the problem with the following code?

```
```
#!/bin/bash
clear
declare name="Bob"
if [ "$name" -eq "Tom"]
echo "Hello Tom"
fi
```
```

**Answer**: The `if` statement is missing the `then` keyword.

+   2. What's the problem with the following code?

```
```
#!/bin/bash
clear
declare name="Bob"
while "$name" == "Tom"
do
echo "Hello Tom"
done
```
```

**Answer**: You must enclose the expression `$name == "Tom"` within brackets:

```
```while [ "$name" -eq "Tom"]```
```

+   3. What's the problem with the following code?

```
```
#!/bin/bash
clear
declare name="Bob"
if [ "$name" -eq "Tom"]
then
	echo "Hello Tom"
if [ "$name" -ne "Tom"]
then
	echo "You're not Tom."
fi
```
```