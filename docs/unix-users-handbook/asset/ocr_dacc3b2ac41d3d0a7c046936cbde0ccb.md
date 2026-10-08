+   ables prohibits functions in other source files from accessing the variable.
3. A variable can be accessible from other source files if it is declared outside all functions, static is not used, and it is accessed from functions in other source files using the qualifier extern. The variable needs a declaration in each of the source files. One will have the variable declaration, and all others will have the declaration with the extern qualifier.

# Typedef

Typedef allows a programmer to assign their names to data types. The convention is uppercase letters are used for names so that they are easily distinguishable. For example, some programs may use bytes in their logic. A programmer may want to declare every variable used as a byte as an unsigned char. It would be easier to use the typedef keyword and assign the word BYTE to the data type unsigned char with the following statement:

```
typedef unsigned char BYTE;
```

Variables can be declared as:

```
BYTE initial_byte;
BYTE new_byte;
```

Essentially, any variable declared as type BYTE is really declared as unsigned char. This will help with organization and program readability.

# Enumerations

Enumerations provide the ability to create a variable that has a limited set of possible values that can be referred to by name. When defining an enumeration, the result will be a list of named integer con-