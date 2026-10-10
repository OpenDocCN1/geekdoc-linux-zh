| 类型 | 字节 | 范围/精度 |
| :--- | :--- | :--- |
| Int | 16 | -32767 to 32767 |
| unsigned int | 16 | 0 to 65535 |
| long int | 32 | -2147483647 to 2147483647 |
| unsigned long int | 32 | 0 to 4294967295 |
| Float | 32 | 6-digit precision |
| Double | 64 | 10-digit precision |
| long double | 80 | 10-digit precision |

# **Declaring a Variable**

All variables in a C program must be declared before they can be used. The general form of a variable definition is:

```
type name;
```

So, for example, to declare a variable x, of data type int so that it may store a value in the range -32767 to 32767, you use the statement:

```
int x;
```

Character strings may also be declared as arrays of characters:

```
char name[number_of_elements];
```

To declare a string called *name* that is 30 characters in length, you would use the following declaration:

```
char name[30];
```

Arrays of other data types may be declared in one, two, or more dimensions as well. For example, to declare a two-dimensional array of integers, you would use:

```
int x[10] [10];
```

The elements of this array are accessed as:

```
x[0][0]
x[0][1]
x[n][n]
```

There are three levels of access to variables; local, module, and global. A variable declared within a code block is known only to the statements within that code block. A variable declared outside any function code blocks, but prefixed with the storage modifier “static,” is known only to the statements within that source module. A variable declared outside any functions, and not prefixed with the static storage type modifier, may be accessed by any statement within any source module of the program. For example: