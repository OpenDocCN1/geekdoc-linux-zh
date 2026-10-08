find the lowest grade, the whole array is passed into the function minimum_grade():

```
lowest = minimum_grade(grades);
```

The function definition looks like:

```
```
int minimum_grade(int all_grades[5])
{
        /* statements */
                ...
        return ( minimum );
}
```
```

The function definition does not need the array size included. The array in the function definition can also be declared as int all_grades[].

Arrays are useful structures; this section covered a beginner’s view.

# # Strings

As previously discussed in the “Data Types” section of this chapter, strings allow us to “string” together characters into words or sentences. A string is not one of the basic data types, but is a rather special type of character array.

A string and a character array are not the same. A string is a character array containing a sequence of character values that end with a null value (`‘\0’`). A character array does not have to contain a string; it can be an array of character values, none of which are null. The following is an array of characters:

```
char array_of_chars[5] = { ‘h’, ‘e’, ‘l’, ‘l’, ‘o’ };
```

The following is an array containing a string:

```
char string_array[6] = "hello";
```