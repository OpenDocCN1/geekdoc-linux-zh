The prototype for this function can be found in the string.h header file. When using any string library function, be sure to include the following processor directive at the top of your source file:

```
#include <string.h>
```

There are many more string functions not addressed in this section.

# Structures

Arrays allow information of the same data type to be grouped together and the contents referenced using subscripts.

C also provides a tool called for grouping information together called structures. *Structures* provide a way to group information of different data types together so that they can be handled as a single entity.

What are the reasons for using a structure? They are several. Structures allow a programmer to organize logically related data items under a common name in a common memory structure. For example, grouping together personal information regarding an employee makes sense. An employee has a name, address, salary, benefits, job title, and so on. Each piece of data is logically related to an employee, but is made up of different data types.

Structures also minimize the number of arguments passed into a function. If a function wanted to print all the information it has on an employee, each piece of data would require an argument; name, address, salary, and so on. When all this information is grouped under a structure, only the structure is passed into a function.

Structures are great tools for enhancing readability. If a program grouped all its employee information into one data structure, it would be easy to find.

A structure is declared using the following syntax:

```
struct tag {
```