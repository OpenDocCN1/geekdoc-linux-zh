
| asort( s [ , d ] ) | Sort the data element values in an array s. The resulting array contains the index values replaced with sequential numbers indicating the new sort order. Alternatively, the new sorted array is stored in array d if specified. |
|---|---|
| asorti( s [ , d ] ) | Sort an array s based on the index values. The resulting array contains the index values as the data element values, with sequential number indexes indicating the sort order. Alternatively, the new sorted array is stored in array d if specified. |
| gensub( r , s , h [ , t ] ) | Search either the variable $0 , or the target string t if supplied, for matches of the regular expression r . If h is a string beginning with either g or G, replaces the matching text with s . If h is a number, it represents which occurrence of r to replace. |
| gsub( r , s [ , t ] ) | Search either the variable $0 , or the target string t if supplied, for matches of the regular expression r . If found, substitute the string s globally. |
| index( s , t ) | Returns the index of the string t in string s, or 0 if not found. |
| length([ s ] ) | Returns the length of string s , or if not specified, the length of $0 . |
| match( s , r [ , a ] ) | Returns the index of the string s where the regular expression r occurs. If array a is specified, it contains the portion of s that matches the regular expression. |
| split( s , a [ , r ] ) | Splits s into array a using either the FS (field separator) character, or the regular expression r if supplied. Returns the number of fields. |
| sprintf( format , variables ) | Returns a string similar to the output of printf using the format and variables supplied. |
| sub( r , s [ , t ] ) | Search either the variable $0 , or the target string t , for matches of the regular expression r . If found, substitutes the string s for the first occurrence. |
| substr( s , i [ , n ] ) | Returns the nth character substring of s , starting at index i. If n is not supplied, the rest of s is used. |
| tolower( s ) | Converts all characters in s to lowercase. |
| toupper( s ) | Converts all characters in s to uppercase. |

Some of the string functions are relatively self explanatory:

```
$ gawk 'BEGIN{x = "testing"; print toupper(x); print length(x) }'
TESTING
7
$
```

However, some of the string functions can get pretty complicated. The asort and asorti functions are new gawk functions that allow you to sort an array variable based on either the data element values (asort) or the index values (asorti). Here’s an example of using asort:

```
$ gawk 'BEGIN{
> var["a"] = 1
> var["g"] = 2
> var["m"] = 3
> var["u"] = 4
> asort(var, test)
> for (i in test)
> print "Index:" ,i," - value:" ,test[i]
> }'
Index: 4 - value: 4
Index: 1 - value: 1
Index: 2 - value: 2
Index: 3 - value: 3
$
```

The new array, test , contains the newly sorted data elements of the original array, but the index values are now changed to numerical values, indicating the proper sort order.

The split function is a great way to push data fields into an array for further processing:

```
$ gawk 'BEGIN{ FS=", " }{
> split($0, var)
> print var[1], var[5]
> }' data1
data11 data15
 data21 data25
 data31 data35
$
```

The new array uses sequential numbers for the array index, starting with index value 1 containing the first data field.

## Time functions

The gawk programming language contains a few functions to help you deal with time values, shown in Table 22.6.

### TABLE 22.6 The gawk Time Functions

| **Function** | **Description** |
| :--- | :--- |
| mktime( *datespec* ) | Converts a date specified in the format YYYY MM DD HH MM SS [DST] into a timestamp value |
| strftime( *format [*, *timestamp*] )* | Formats either the current time of day timestamp, or timestamp if provided, into a formatted day and date, using the date() shell function format |
| systime() | Returns the timestamp for the current time of day |

The time functions are often used when working with log files that contain dates that you need to compare. By converting the text representation of a date to the epoch time (the number of seconds since midnight, January 1, 1970), you can easily compare dates.

The following is an example of using the time functions in a gawk program:

```
$ gawk 'BEGIN{ 
> date = systime() 
> day = strftime("%A, %B %d, %Y", date) 
> print day 
> }' 
 Friday, December 26, 2014 
$ 
```

This example uses the systime function to retrieve the current epoch timestamp from the system and then uses the strftime function to convert it into a human readable format using the shell command's date format characters.

## Trying Out User-Defined Functions

You're not limited to just using the built-in functions available in *gawk*. You can create your own functions for use in your *gawk* programs. This section shows you how to define and use your own functions in your *gawk* programs.

### Defining a function

To define your own function, you must use the *function* keyword:

```
function *name*((*variables*))
{
   *statements*
}
```

The function *name* must uniquely identify your function. You can pass one or more variables into the function from the calling *gawk* program:

```
function printthird()
{
   print $3
}
```

This function will print the third data field in the record. The function can also return a value using the *return* statement:

```
*return* *value*
```

The *value* can be a variable, or an equation that evaluates to a value:

```
function myrand(limit)
{
   *return* int(limit * rand())
}
```

You can assign the *value* *returned* from the function to a variable in the *gawk* program:

```
x = myrand(100)
```

The variable will contain the value returned from the function.

### Using your functions

When you define a function, it must appear by itself before you define any programming sections (including the `BEGIN` section). This may look a little odd at first, but it helps keep the function code separate from the rest of the `awk` program:

```
$ awk '
> function myprint()
> {
>	printf "%-16s - %s\n", $1, $4
> }
> BEGIN{FS="\n"; RS=""}
> {
>	myprint()
> }' data2
Ima Test      - (312)555-1234
Frank Tester  - (317)555-9876
Haley Example - (313)555-4938
$
```

The function defines the `myprint( )` function, which formats the first and fourth data fields in the record for printing. The `awk` program then uses the function to display the data from the data file.

Once you define a function, you can use it as often as necessary in the program section of the code. This saves lots of work when using long algorithms.

### Creating a function library

Obviously, having to rewrite your `awk` functions every time you need them is not all that pleasant of an experience. However, `awk` provides a way for you to combine your functions into a single library file that you can use in all your `awk` programming.

First, you need to create a file that contains all your `awk` functions:

```
$ cat funclib
function myprint()
{
	printf "%-16s - %s\n", $1, $4
}
function myrand(limit)
{
	return int(limit * rand())
}
function printthird()
{
    print $3
}
$
```

The `funclib` file contains three function definitions. To use them, you need to use the `-f` command line parameter. Unfortunately, you can't combine the -f command line parameter with an inline `gawk` script, but you can use multiple -f parameters on the same command line.

Thus, to use your library, just create a file that contains your `gawk` program, and specify both the library file and your program file on the command line:

```
$ cat script4
BEGIN{ FS="\n"; RS=""}
{
    myprint()
}
$ gawk -f funclib -f script4 data2
Ima Test      - (312)555-1234
Frank Tester  - (317)555-9876
Haley Example - (313)555-4938
$
```

Now all you need to do is add the `funclib` file to your `gawk` command line whenever you need to use a function defined in the library.

### Working Through a Practical Example

The advanced `gawk` features come in handy if you have to handle data values in a data file, such as tabulating sales figures or calculating bowling scores. When you work with data files, the key is to first group related data records together and then perform any calculations required on the related data.

For example, let's work with a data file that contains the bowling scores from a game between two teams, each with two players:

```
$ cat scores.txt
Rich Blum,team1,100,115,95
```
