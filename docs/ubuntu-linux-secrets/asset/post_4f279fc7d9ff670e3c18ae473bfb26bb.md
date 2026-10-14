
## Using Variables in Perl

Just like in shell scripts, Perl uses variables to store data within the script. Once you store a value in a variable, Perl retains that value so you can use it later in the script. There are three types of variables available in Perl:

- Scalar
- Array
- Hash (also called associative array)

The following sections describe each of these types of variables, and show how to use them.

## Scalar Variables

Scalar variables hold a single data value. Unlike in shell scripts, scalar variables are always preceded by a dollar sign. To place a value in a variable requires an assignment statement:

```
$variable = value;
```

Some assignment statement examples using scalar variables are:

```
$x = 10;
$pi = 3.14159;
$value1 = $value2;
$pet = "cat";
```

Scalar variables can hold text strings, integer numbers, or floating-point numbers, and can change from one type to the other, depending on the operator. If an operator expects a number, Perl will use the value as a number, and if an operator expects a string, Perl will use the value as a string. Unlike some more formal programming languages that require you to define a data type for a variable ahead of time, then only use that type of data for that variable, Perl lets you use any type of data type in a variable at any time in your code.

Whenever you reference the scalar variable in the Perl script, Perl uses the value stored in the variable. Here's a demonstration of that:

```
$ cat test3.pl
#!/usr/bin/perl
# testing Perl scalar variables
$test = "Jessica";
$pi = 3.14159;
$radius = 5;
$area = $pi * $radius ** 2;
print "$test says the area should be $area\n";
$ chmod +x test3.pl
$ ./test3.pl
Jessica says the area should be 78.53975
$
```

The Perl script calculated the formula (including using the floating-point values) and used the print statement to display the output. If you've done any programming in higher-level programming languages such as Java or C, you'll notice how nice it is in Perl to be able to use a variable that contains a numerical value in a print statement without

having to reformat the value to a string. Perl automatically uses the numerical value as a string for us.

## Array Variables

Arrays are indexed lists of scalar data. Each index is an integer value, starting at 0 and incrementing through however many elements are stored in the array. You identify an array variable by using the @ sign in front of the variable name instead of a dollar sign. An example of creating an array variable and assigning values to it is:

```
@days = ("Monday,", "Tuesday,", "Wednesday,", "Thursday,", "Friday");
```

Notice that the array definition is enclosed in parentheses, and a comma separates each value. The tricky part about arrays is trying to reference a single data value from within the array. To retrieve an individual value, you must use the dollar sign in front of the array variable name, plus add the index that references the value you want to retrieve within square brackets, like this:

```
$array[index]
```

For example, if you need to retrieve the second value stored in the @days array, you'd use the format:

```
print "Today is $days[1]\n";
```

Because the array index starts at zero, the 1 value references the second data value (Tuesday in this example) in the array. Here's a short script that demonstrates using array variables in a Perl script:

```
$ cat test4.pl
#!/usr/bin/perl
# testing arrays in Perl
@days = ("Monday,", "Tuesday,", "Wednesday,", "Thursday,", "Friday");

print "I always have practice on $days[2]\n";
print "I'm not sure what we're doing on $days[4]\n";
$ chmod +x test4.pl
$ ./test4.pl
I always have practice on Wednesday
I'm not sure what we're doing on Friday
$
```

The script replaced the array variable with the appropriate element value stored in the array.

## Hash Variables

Hashes (also known as associative arrays) are collections of scalar values arranged in key/value pairs, similar to an array. The difference is that in hashes, the key is a text string instead of a numerical index. This allows you to relate one word with another. You retrieve the data value stored in the hash based on the key value.

Hashes are identified with a percent sign instead of a dollar sign. An example of a creating a hash is:

```
%favorites = ("fruit" => "banana,", "vegetable" => "carrot");
```
