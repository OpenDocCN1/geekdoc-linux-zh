# **OPINION CODING**

# Power of two

When it comes to computers, nothing beats binary arithmetic. Here's how to find out if an integer is a power of two

> > Identifying whether or not a given positive integer is a power of two is not a challenging job, but it needs a lot of processing, especially if the integer is larger than 2^20. Also, it highlights that: a) you should always think carefully before implementation, and b) it is good to have a sound knowledge of mathematics when you are programming. The more areas of mathematics you know, the better.
> 
> Here is a standard, brute force and recursive Python function (power0f2.py) that solves the initial problem:

```
```
def powerOf2(num):
    if (num == 1):
        return True
    elif (num == 0) or (num % 2 == 1):
        return False
    else:
        return powerOf2(num / 2)
```
```

Another version uses binary arithmetic (bitwise.py):

```
```
def powerOf2(number):
    return (number & (number-1) == 0) and (number != 0)
```
```

Put simply, the function checks whether there is more than one "1" bit set in the binary representation of the number variable. As you know, CPUs calculate using binary arithmetic. These calculations are especially fast and happen quicker than any other kind.

To make the algorithm clearer: the binary representation of 64, which is a power of two, is 1000000. 64-1 equals 63, the binary representation of 63 is 0111111. So (1111111 & 1000000) equals 0, which proves that number 64 is a power of two. The drawback is when a solution that uses binary arithmetic is only suitable for problems that have to deal with powers of two.

The following Python script generates 1,000,000 random numbers that will then be used as input for testing the two techniques:

```
```
#!/usr/bin/python
import random
MIN = 0
MAX = 100000
TOTAL = 1000000
```
```

![](bbox=[0.43, 0.35, 0.61, 0.52])

**Mihalis Tsoukalos** is a UNIX administrator, a programmer, a DBA and a mathematician. He has used Linux since 1993

> > "It is good to have a sound knowledge of mathematics when you are programming. The more areas of mathematics you know, the better"

```
```python
for i in range(0, TOTAL):
    print random.randrange(MIN, MAX)
```
```

Although the function **random.randrange()** suggests it produces random numbers, their statistical distribution is not so random after all. The following output proves it:

```
```
$ awk '{ if ($0 > 0 && $0 < 10000) print }' numbers | wc -l
99585
$ awk '{ if ($0 > 10000 && $0 < 20000) print }' numbers | wc -l
99811
$ awk '{ if ($0 > 20000 && $0 < 30000) print }' numbers | wc -l
99930
```
```

The following can find out if there are duplicate numbers:

```
```
$ sort numbers | uniq -c | sort -rn
```
```

Having duplicates is not a bad thing, it's just good to know. It is now time to perform the actual benchmarking. This time the benchmarking will be done using the **time()** Python function. As you can see in the Python code, each program repeats itself ten times to produce even more accurate results. The results are as follows:

```
```
powerOf2.py: 12.287568 seconds
bitwise.py: 8.285457 seconds
```
```

Although the difference is only four seconds, it took powerOf2.py 50% more time than bitwise.py to perform exactly the same task.

The maximum permitted integer plays a central role in the problem because if it is small, the brute force technique will obviously take less time. The maximum integer that can be found in the sample was set to 1000 for the following results:

```
```
powerOf2.py: 11.39706 seconds
bitwise.py: 8.412941 seconds
```
```

You can find the source code at github.com/mactsousk and fileso.co.uk/linuxuser-157.