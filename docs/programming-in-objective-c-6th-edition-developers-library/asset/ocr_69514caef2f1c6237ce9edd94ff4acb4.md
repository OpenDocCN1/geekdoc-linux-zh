a structure called i is defined to contain two integer pointers, the first one called p and the second one p . You can define a variable of type s in the usual way:

The variable p can now be used in the normal fashion, remembering that p itself is not a pointer, but a structure variable that has two pointers as its members.

Program 10.5 shows how the i structure can be handled in a C program.

# Program 10.5 Using Structures Containing Pointers

Click here to view code image

```
```c
/
#
i
{






}
```
```

# Program 10.5 Output

Click here to view code image

```
```
i
i
```
```

After the variables have been defined, the assignment statement

sets the p member of p pointing to the integer variable i , whereas the next statement

sets the p member pointing to i . Next, −9 is assigned to the variable that is pointed to by p . Because you just set this to point to i , −9 is stored in i . No parentheses are needed in this assignment statement because, as mentioned previously, the structure member operator . has higher precedence than the indirection operator. Therefore, the pointer is correctly referenced from the structure before the indirection operator is applied. Of course, parentheses could have been used just to play it safe, as at times it can be difficult to try to remember which of two operators has