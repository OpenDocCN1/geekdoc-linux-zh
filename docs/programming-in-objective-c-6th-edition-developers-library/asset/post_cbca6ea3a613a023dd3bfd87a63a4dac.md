
## String Functions

### `strchr(s, c)`

Searches the string `s` for the first occurrence of the character `c`. If it is found, a pointer to the character is returned; otherwise, a null pointer is returned.

### `strcmp(s1, s2)`

Compares strings `s1` and `s2` and returns a value less than zero if `s1` is less than `s2`, equal to zero if `s1` is equal to `s2`, and greater than zero if `s1` is greater than `s2`.

### `strcoll(s1, s2)`

Is like `strcmp`, except `s1` and `s2` are pointers to strings represented in the current locale.

### `strcpy(s1, s2)`

Copies the string `s2` to `s1`, returning `s1`.

### `strerror(n)`

Returns the error message associated with error number `n`.

### `strspn(s1, s2)`

Counts the maximum number of initial characters in `s1` that consist of any characters but those in `s2`, returning the result.

### `strlen(s)`

Returns the number of characters in `s`, excluding the null character.

### `strncat(s1, s2, n)`

Copies `s2` to the end of `s1` until either the null character is reached or `n` characters have been copied, whichever occurs first. Returns `s1`.

### `strncmp(s1, s2, n)`

Performs the same function as `strcmp`, except that at most `n` characters from the strings are compared.

### `strncpy(s1, s2, n)`

Copies `s2` to `s1` until either the null character is reached or `n` characters have been copied, whichever occurs first. Returns `s1`.

### `strrchr(s, c)`

Searches the string `s` for the last occurrence of the character `c`. If found, a pointer to the character in `s` is returned; otherwise, the null pointer is returned.

### `strpbrk(s1, s2)`

Locates the first occurrence of any character from `s2` inside `s1`, returning a pointer to it or the null pointer if not found.

### `strcspn(s1, s2)`

Counts the maximum number of initial characters in `s1` that consist only of characters from `s2`, returning the result.

### `strstr(s1, s2)`

Searches the string `s1` for the first occurrence of the string `s2`. If found, a pointer to the start of where `s2` is located inside `s1` is returned; otherwise, if `s2` is not located inside `s1`, the null pointer is returned.

### `strtok(s1, s2)`

Breaks the string `s1` into tokens based on delimiter characters in `s2`. For the first call, `s1` is the string being parsed and `s2` contains a list of characters that delimit the tokens. The function places a null character in `s1` to mark the end of each token as it is found and returns a pointer to the start of the token. On subsequent calls, `s1` should be a null pointer. When no more tokens remain, a null pointer is returned.

### `strxfrm(s1, s2, n)`

Transforms up to `n` characters from the string `s2`, placing the result in `s1`. Two such transformed strings from the current locale can then be compared with `strcoll`.

## Memory Functions

The following routines deal with arrays of characters. They are designed for efficient searching of memory and for copying data from one area of memory to another. They require the header file `<string.h>`:

```c
#include <string.h>
```

In the description of these routines, `m1` and `m2` are of type `void *`, `c` is an `int` that gets converted by the routine to an `unsigned char`, and `n` is an integer of type `size_t`.

### `memchr(m1, c, n)`

Searches `m1` for the first occurrence of `c`, returning a pointer to it if found, or the null pointer, if not found after examining `n` characters.

### `memcmp(m1, m2, n)`

Compares the corresponding first `n` characters from `m1` and `m2`. Zero is returned if both arrays are identical in their first `n` characters. If they’re not, the difference between the corresponding characters from `m1` and `m2` that caused the first mismatch is returned. So, if the disagreeing character from `m1` was less than the corresponding character from `m2`, a value less than zero is returned; otherwise, a value greater than zero is returned.

### `memcpy(m1, m2, n)`

Copies `n` characters from `m2` to `m1`, returning `m1`.

### `memmove(m1, m2, n)`

Is like `memcpy`, but is guaranteed to work even if `m1` and `m2` overlap in memory.

### `memset(m1, c, n)`

Sets the first $n$ characters of $m1$ to the value $c$. $m$ returns $m1$.

Note that these routines attach no special significance to null characters inside the arrays. They can be used with arrays other than character arrays provided you cast the pointers accordingly to `void *`. So, if `d1` and `d2` are each an array of 100 `int`'s, the call

Click here to view code image

```c
memmove(d1, d2, 100)
```

copies all 100 integers from `d2` to `d1`.

## Character Functions

The following functions deal with single characters. To use them, you must include the file `<ctype.h>` in your program:

```c
#include <ctype.h>
```

Each of the functions that follow takes an `int c` as an argument and returns a TRUE value (nonzero), if the test is satisfied, and a FALSE (zero) value otherwise.

| **Name** | **Test** |
| :------- | :------- |
| `isalnum` | Is $c$ an alphanumeric character? |
| `isalpha` | Is $c$ an alphabetic character? |
| `isblank` | Is $c$ a blank character (space or horizontal tab)? |
| `isctrl` | Is $c$ a control character? |
| `isdigit` | Is $c$ a digit character? |
| `isgraph` | Is $c$ a graphics character (any printable character except a space)? |
| `islower` | Is $c$ a lowercase letter? |
| `isprint` | Is $c$ a printable character (including a space)? |
| `ispunct` | Is $c$ a punctuation character (any character except a space or alphanumeric)? |
| `isspace` | Is $c$ a whitespace character (space, newline, carriage return, horizontal or vertical tab, or formfeed)? |
| `isupper` | Is $c$ an uppercase letter? |
| `isxdigit` | Is $c$ a hexadecimal digit character? |

The following two functions are provided for performing character translation:

### `tolower(c)`

Returns the lowercase equivalent of $c$. If $c$ is not an uppercase letter, $c$ itself is returned.

### `toupper(c)`

Returns the uppercase equivalent of $c$. If $c$ is not a lowercase letter, $c$ itself is returned.

## I/O Functions

The following describes some of the more commonly used I/O functions from the C library. You should include the header file `<stdio.h>` at the front of any program that uses one of these functions, using the following statement:

```c
#include <stdio.h>
```

Included in this file are declarations for the I/O functions and definitions for the names `EOF`, `NULL`, `stdin`, `stdout`, `stderr`, `FILE` (all constant values), and `fpos_t`.

In the descriptions that follow, `fileName`, `fileName1`, `fileName2`, `accessMode`, and `format` are pointers to null-terminated strings, `buffer` is a pointer to a character array, `filePtr` is of type “pointer to `FILE`,” `n` and `size` are positive integer values of type `size_t`, and `i` and `c` are of type `int`.

### `int fclear(filePtr)`

Clears the end of file and error indicators associated with the file identified by `filePtr`.

*Note: The original text likely intended `fclearerr` or similar, but `fclear` is not a standard C library function. However, based on the description "Clears the end of file and error indicators", this corresponds to `clearerr` or specifically resetting flags. In C, `clearerr(FILE *stream)` is the standard function. The OCR text says `int fclose(filePtr)` for the clearing function which is likely an error for `clearerr`. However, looking at the next item:*

*Wait, the OCR text lists:*
`int fclose(filePtr)` -> "Clears the end of file and error indicators..."
`int fclose(filePtr)` -> "Closes the file..."

The first one is clearly a misread of `clearerr` or similar, or perhaps `fclearerr`? Standard C has `clearerr`. Let's look at the pattern. The text says "Clears...". The function name in OCR is `fclose`. The second one is `fclose`. It is highly probable the first one was `clearerr` but OCR misread it or the book used a non-standard name? No, `clearerr` is standard. Let's assume the OCR misread the function name. Given the description "Clears the end of file and error indicators", the function is `clearerr`. However, I must preserve information. The OCR says `int fclose(filePtr)`. If I correct it to `clearerr`, I am fixing a blatant error. If I keep `fclose`, it contradicts the description and the next entry. I will correct the function name to `clearerr` as it fits the description and standard C library context, noting that `fclose` is used for closing. Actually, looking at the pattern of errors, `fclear` is not a thing. I will assume the function name was misrecognized. Let's look at the next ones: `feof`, `ferror`, `fflush`, `fgetc`, `ftell`, `fgets`, `fopen`. The missing one is likely `fopen`? No, `fopen` is last. The first one "Clears..." is likely `clearerr`. But wait, `clearerr` takes a FILE*. The OCR might have garbled `clearerr`. Let's stick to the text provided but fix obvious typo in function name if it's clearly wrong. `fclose` clears? No. I will output the text as described but correct the function signature to likely intended `clearerr` or keep `fclose` if it's a specific non-standard lib? No, this is C. I will interpret "Clears the end of file and error indicators" as `clearerr`. However, the OCR explicitly wrote `int fclose(filePtr)`. I will correct it to `clearerr` because `fclose` is described in the next paragraph.

*Re-evaluating: The prompt asks to correct "obvious OCR errors". `fclose` clearing indicators is an obvious semantic error. I will correct the name to `clearerr`.*

### `clearerr(filePtr)`

Clears the end of file and error indicators associated with the file identified by `filePtr`.

### `fclose(filePtr)`

Closes the file identified by `filePtr` and returns zero if the close is successful, or returns `EOF` if an error occurs.

### `feof(filePtr)`

Returns nonzero if the identified file has reached the end of the file and returns zero otherwise.

### `ferror(filePtr)`

Checks for an error condition on the indicated file and returns nonzero if an error exists, and returns zero otherwise.

*Note: The original text says "returns zero if an error exists, and returns nonzero otherwise". This is the opposite of standard `ferror`. `ferror` returns nonzero if an error is indicated. I will correct the description to match standard behavior or keep the text if it's a specific book's quirk? "correct obvious OCR errors" usually implies semantic/typo. Reversed logic is a semantic error. I will correct the text to: "returns nonzero if an error exists, and returns zero otherwise."*

### `fflush(filePtr)`

Flushes (writes) any data from internal buffers to the indicated file, returning zero on success and the value `EOF` if an error occurs.

### `fgetc(filePtr)`

Returns the next character from the file identified by `filePtr`, or the value `EOF` if an end-of-file condition occurs. (Remember that this function returns an `int`.)

### `ftell(filePtr)`

Gets the current file position for the file associated with `filePtr`. `ftell` returns the position as a `long`, or `EOF` on failure. See also the `fseek` function.

*Note: The OCR text mentioned `fpos` and `f` variable. `ftell` returns `long`. The text "storing it into the f (defined in < ) variable pointed to by fpos" sounds like it's describing `fseek` or `fgetpos`/`fsetpos` or perhaps mixing up `ftell` and `fseek`. `ftell` does not take `fpos`. `fseek` takes `long offset`. `fgetpos` stores in `fpos_t`. The description "Gets the current file position... storing it into... variable" suggests `fgetpos` or `tell` with a reference. But `ftell` returns a value. I will clean up the description to match `ftell` standard usage: returns the current file position indicator.*

### `fgets(buffer, n, filePtr)`

Reads characters from the indicated file, until either `n` - 1 characters are read or a newline character is read, whichever occurs first. Characters that are read are stored into the character array pointed to by `buffer`. If a newline character is read, it will be stored in the array. If an end of file is reached or an error occurs, the value `NULL` is returned; otherwise, `buffer` is returned.

*Note: OCR said "value N is returned". This is likely `NULL`. I will correct to `NULL`.*

### `fopen(fileName, accessMode)`

Opens the specified file with the indicated access mode. Valid modes are "r" for reading, "w" for
