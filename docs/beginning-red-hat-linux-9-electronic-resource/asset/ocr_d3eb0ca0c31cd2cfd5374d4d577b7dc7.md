A shorter form of this construct is the if then . . fi construct shown below:

```
if expression
then
statement 1
statement 2
...
statement n
fi
```

This construct is useful when we need to execute certain statements only if a certain condition is met. Below is a sample script that uses the if then . . fi form:

```
#!/bin/sh
x=10
y=5

if [ "$x" -eq "$y" ]
then
echo "The two numbers are equal"
fi
```

*Note that in both cases the statements are indented only to make the code more readable and this is not a requirement.*

# # Loops

In this section we shall look at looping constructs that allow us to conditionally execute a set of statements repeatedly.

The for loop is essentially a simple looping construct that allows us to specify a set of statements that need to be executed a certain number of times:

```
#!/bin/sh
for fil in `ls *.txt`
do
cat $fil >> complete.txt
done
```

The script above concatenates all the text files in the current directory into one large text file.

```
#!/bin/sh
for number in 1 2 3 4 5
do
echo $
done
```