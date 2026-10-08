Another good example of an array is this prime-number builder:

This program builds an array of prime numbers and then uses it to determine further primes.
The output is

% primes
2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89 97x

| SUMMARY | In this task, you were introduced to arrays. Arrays provide a means of relating common data. The most common use is to create a string, which is just an array of characters. |

# Task 24.7: Pointers

| DESCRIPTION | Each variable in a C program has a given location in memory. That location, or address, can be assigned to a pointer. |

| ACTION | To understand pointers, you first need to understand how memory is organized. Every time you declare a variable, a piece of memory is allocated in a given size, and is labeled with your variable name. Any time you access that name, the value of the data at that location is provided. |

So, when you declare

```
int i;
```