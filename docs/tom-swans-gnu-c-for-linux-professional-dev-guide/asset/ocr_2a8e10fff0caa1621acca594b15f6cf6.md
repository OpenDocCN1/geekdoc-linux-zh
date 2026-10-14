# CHARACTERS

Use the char type to create variables that can hold individual characters. For example, the following statement creates a char variable c and assigns it the letter Q:

```
char c = 'Q';
```

Delimit single literal characters with single quotes (the apostrophe character on most PC keyboards). As mentioned, the char type is internally just an integer value. Because 81 is the letter Q's ASCII value, the following is equivalent to the preceding statement:

```
char c = 81;
```

# C-STYLE STRING CONSTANTS

A C-style string constant is a series of one or more chars, each taking one byte in memory, and ending with a null character, equal to ASCII 0. Quote literal strings using double quote marks. For example, you might define a constant named TITLE associated with a literal string like this:

```
#define TITLE "My Program"
```

You can then write the program's title to the console, and start a new line, using the following statement:

```
cout << TITLE << endl;
```

# C-STYLE STRING VARIABLES

A C-style string variable typically holds user input—for example, a filename. Use the char type to create a C-style string variable with a statement such as

```
char filename[] = "datafile.txt";
```

The square brackets tell the compiler that filename is an array of multiple characters. The size of the array equals the number of characters in the quoted string plus one for a terminating null. Precede the declaration with const to create a constant string that cannot be changed at runtime:

```
const char mypath[] = "/home/username";
```