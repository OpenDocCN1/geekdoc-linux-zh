# 398 Part III ♦ Using the Command Line in SUSE Linux

This tells the system that the interpreter needed to run the script is bash. If you source the script, this is not necessary.

```
fred@bible:-> chmod +x scr1.sh
fred@bible:-> ./scr1.sh
Hello fred
Your current directory is /home/fred
```

A shell script can include the types of logical structures that one would expect to find in any programming language. For example, a for loop:

```
#!/bin/bash
for i in 1 2 3 4 5
do
echo $i
done
```

Here $i represents the variable i, which takes the successive values in the loop.

Save this as scr2.sh, make it executable, and run it as you have previously, and you'll see the following:

```
fred@bible:-> chmod +x scr2.sh
fred@bible:-> ./scr2.sh
1
2
3
4
5
```

Although you are unlikely to use numerical variables often as basic counters in keeping track of a repeating process, you can do arithmetic in shell scripts:

```
#!/bin/bash
a=12
echo "a is $a"
echo "a+1 is $((a+1))"
```

This script produces output like this:

```
a is 12
a+1 is 13
```

> Note that there should be no white space around the = sign; if there is, the variable will not be assigned. Notice also the way that extra brackets were needed in $((a+1)).

![](bbox=[0.125, 0.796, 0.181, 0.853])