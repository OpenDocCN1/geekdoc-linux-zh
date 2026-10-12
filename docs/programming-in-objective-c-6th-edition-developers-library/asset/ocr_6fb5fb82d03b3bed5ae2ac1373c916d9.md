```
/
#
v
{



}
i
{


}
```

# **Program 9.1 Output**

T

The first `for` loop inside the `concatenate` function copies the characters from the `source` array into the `result` array. This loop is executed `n` times, which is the number of characters contained inside the `source` array.

The second `for` loop copies `source` into the `result` array. Because `source` was `n` characters long, copying into `result` begins at `result[n]`—the position immediately following the one occupied by the last character of `source`. After this `for` loop is done, the `result` array contains the `n` characters representing `source` concatenated to the end of `source`.

Inside the `main` routine, two `char` arrays, `source` and `target`, are defined. The first array is initialized to the characters `'1'`, `'2'`, `'3'`, `'4'`, and `' '`. This last character represents a blank space and is a perfectly valid character constant. The second array is initially set to the characters `'a'`, `'b'`, `'c'`, `'d'`, and `' '`. A third character array, `result`, is defined with enough space to hold `source` concatenated to `target`, or 11 characters. It is not declared as a `const` array because its contents will be changed.

The function call

```c
call
```
calls the `concatenate` function to concatenate the character arrays `source` and `target`, with the destination