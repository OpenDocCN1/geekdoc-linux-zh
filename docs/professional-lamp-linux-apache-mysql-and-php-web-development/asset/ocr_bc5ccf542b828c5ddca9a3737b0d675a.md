# Chapter 3

```
```
$matrix = array(array(1, 2), array(3, 4));
$temp = $matrix;
array_push(null, $temp);
$transposed_matrix = call_user_func_array('array_map', $temp);
```
```

The first argument to `array_map()` is the name of the callback function, so make the first argument of `$temp` that callback (in this case, a null callback). This is why I needed the temp variable; `array_push()` modifies the original array rather than returning a copy. I could have lived dangerously by using `$transposed_matrix` itself instead of `$temp`, and saved myself the variable and the final `unset()`. Dangerous, because it would have reduced the readability of the code slightly (creating the variable as one thing (the list arguments to `array_map()`), and two lines later using it for something quite different (the result of the `array_map()` call).

```
```
$temp = array(null, array(1,2), array(3,4));
$transposed_matrix = call_user_func_array('array_map', $temp);
```
```

Here’s the result of carrying out `call_user_func_array()` by hand.

```
```
$transposed_matrix = array_map(null, array(1,2), array(3,4));
```
```

So one way to look at the operation of `call_user_func('foo', array(arguments))` is to look on it as taking an array and replacing `array(arguments)` with `foo(arguments)`.

To complete the example, evaluate the `array_map()` call:

```
```
$transposed_matrix = array(array(1,3), array(2,4));
```
```

The practical upshot of `call_user_func_array()` is that you can store all of the arguments to a function in a single array, without needing to know how many arguments there are (consider that several PHP functions accept variable numbers of arguments, and so can yours), nor needing to take each of the elements out of the array and inserting them into the function call by hand.

The reason for the slightly long-winded name is that there is also a `call_user_func()` function. Instead of taking a callback and its arguments as an array, it takes the callback and its arguments *explicitly*. Just as you can think of PHP as converting `call_user_func_array('foo', array(arguments))` to `foo(arguments)`, `call_user_func('foo', arguments)` converts to `foo(arguments)` without using the intermediate array.

It may sound as though it’s effectively the same as putting `'foo'` into a variable `$func`, and then writing `$func(...)`. And for ordinary functions, it is. But for object methods it’s another story. Try it:

```
```
<?php
class foo
{

 public function bar($a, $b)
 {
   echo "I'm here! $a! $b! And all that!";
 }
}
```
```