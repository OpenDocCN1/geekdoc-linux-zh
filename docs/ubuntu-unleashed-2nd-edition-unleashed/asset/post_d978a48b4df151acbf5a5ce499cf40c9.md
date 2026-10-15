
```php
<?php
$ourstring = "The Quick Brown Fox Jumped Over The Lazy Dog";
if (strpos($ourstring, "The")) {
    echo "Found 'The'!\n";
} else {
    echo "'The' not found!\n";
}
?>
```

Note that we have temporarily taken out the leading and trailing whitespace from `$ourstring` and we are using the return value of `strpos()` for our conditional statement. This reads, “If the string is found, then print a message; if not, print another message.” Or does it?

Run the script, and you will see it print the “not found” message. The reason for this is that `strpos()` returns false if the substring is not found and otherwise returns the position where it starts. If you recall, any nonzero number equates to true in PHP, which means that 0 equates to false. With that in mind, what is the string index of the first `The` in our phrase? Because PHP’s strings are zero based and we no longer have the spaces on either side of the string, the `The` is at position 0, which causes our conditional statement to evaluate to false—hence, the problem.

The solution here is to check for identity. We know that 0 and false are equal, but they are not identical because 0 is an integer, whereas false is a Boolean. So, we need to rewrite the conditional statement to see whether the return value from `strpos()` is identical to false. If it is, the substring was not found:

```php
<?php
$ourstring = "The Quick Brown Fox Jumped Over The Lazy Dog";
if (strpos($ourstring, "The") !== false) {
    echo "Found 'The'!\n";
} else {
    echo "'The' not found!\n";
}
?>
```

## Arrays

Working with arrays is no easy task, but PHP makes it easier by providing a selection of functions that can sort, shuffle, intersect, and filter them. As with other functions, there is only space here to choose a selection; this is by no means a definitive reference to PHP’s array functions.

The easiest function to use is `array_unique()`, which takes an array as its only parameter and returns the same array with all duplicate values removed. Also in the realm of “so easy you do not need a code example” is the `shuffle()` function, which takes an array as its parameter and randomizes the order of its elements. Note that `shuffle()` does not return the randomized array; it uses your parameter as a reference and scrambles it directly. The last too-easy-to-demonstrate function is `in_array()`, which takes a value as its first parameter and an array as its second and returns true if the value is in the array.

With those out of the way, we can focus on the more interesting functions, two of which are `array_keys()` and `array_values()`. They both take an array as their only parameter and return a new array made up of the keys in the array or the values of the array, respectively. The `array_values()` function is an easy way to create a new array of the same data, just without the keys. This is often used if you have numbered your array keys, deleted several elements, and want to reorder it.

The `array_keys()` function creates a new array where the values are the keys from the old array, like this:

```php
<?php
$myarr = array("foo" => "red", "bar" => "blue", "baz" => "green");
$mykeys = array_keys($myarr);
foreach($mykeys as $key => $value) {
    echo "$key = $value\n";
}
?>
```

That prints "0 = foo", "1 = bar", and "2 = baz".

Several functions are used specifically for array sorting, but only two get much use: `asort()` and `ksort()`, the first of which sorts the array by its values and the second of which sorts the array by its keys. Given the array `$myarr` from the previous example, sorting by the values would produce an array with elements in the order bar/blue, baz/green, and foo/red. Sorting by key would give the elements in the order bar/blue, baz/green, and foo/red. As with the `shuffle()` function, both `asort()` and `ksort()` do their work in place, meaning they return no value, directly altering the parameter you pass in. For interest's sake, you can also use `arsort()` and `krsort()` for reverse value sorting and reverse key sorting, respectively.

This code example reverse sorts the array by value and then prints it as before:

```php
<?php
$myarr = array("foo" => "red", "bar" => "blue", "baz" => "green");
arsort($myarr);
foreach($myarr as $key => $value) {
    echo "$key = $value\n";
}
?>
```

Previously when discussing constants, we mentioned the `extract()` function that converts an array into individual variables; now it is time to start using it for real. You need to provide three variables: the array you want to extract, how you want the variables prefixed, and the prefix you want used. Technically, the last two parameters are optional,
