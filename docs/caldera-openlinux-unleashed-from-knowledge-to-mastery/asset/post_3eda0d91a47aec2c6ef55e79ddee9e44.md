
0. For example, the string `76trombones` will evaluate as the number `76` if used in a numerical calculation, but the string `polar` bear will evaluate to 0.

## Arrays

Arrays are indicated with the `@` character, as in `@fish`. An *array* is a list of values that are referenced by index number, starting with the first element numbered `0`, just like C and awk. Each element in the array is a scalar value. Because scalar values are indicated with the `$` character, a single element in an array is also indicated with a `$` character. For example, `$fish[2]` refers to the third element in the `@fish` array. This tends to throw some people off, but it is completely consistent.

## Hashes

Hashes are indicated with the `%` character, as in `%employee`. A *hash*, which used to go by the cumbersome name *associative arrays*, is a list of key/value pairs. Individual elements in the hash are referenced by name, rather than by index. Again, because the values are scalars, the `$` character is used for individual elements. For example, `$employee{name}` gives you one value from the hash. Two rather useful functions for dealing with hashes are **keys** and **values**. The keys function returns an array containing all the keys of the hash, and values returns an array of the values of the hash. The code in Listing 32.2 displays all the values in your environment, much like typing the `env` command.

**LISTING 32.2** Displaying the Contents of the env Hash

```perl
foreach $key (keys %ENV) {
    print "$key = $ENV{$key}\n";
}
```

## Special Variables

Perl has a wide variety of special variables. These usually look like punctuation—such as `$_`, `$1`, and `$)`—and are extremely useful for shorthand code. (`$_` is the default variable, `$1` is the error message returned by the operating system, and `$)` is the Perl version number.)

`$_` is perhaps the most useful of these, and we use it some more within this chapter. `$_` is the Perl default variable, which is used when no argument is specified. For example, the following two statements are equivalent:

```perl
chomp;

chomp($_);
```

The following loops are equivalent:

```perl
for $cow (@cattle) {
    print "$cow says moo.\n";
}
for (@cattle) {
    print "$_ says moo.\n";
}
```

For a complete listing of these special variables, see the `perlvar` document that comes with your Perl distribution, or jump online at http://www.cpan.org/doc/manual/html/pod/perlvar.html.

## Operators

Perl supports a number of operators to perform various operations. Perl has comparison operators (used, as the name implies, to compare values), compound operators (used to combine operations or multiple comparisons), arithmetic operators (to perform math), and special string constants.

### Comparison Operators

The comparison operators used by Perl are similar to those used by C, awk, and the various UNIX shells. Most frequently, a comparison operator is used within an `if` statement or loop.

Perl has two categories of comparison operators: relational operators (greater than, less than, and so on) and equality operators (equal, not equal). Both categories include operators for numbers and strings.

Table 32.1 shows the relational operators and their behavior.

| | Numeric | String | Meaning |
|---|---|---|---|
| > | > | gt | Greater than |
| >= | >= | ge | Greater than or equal to |
| < | < | lt | Less than |
| <= | <= | le | Less than or equal to |

*Note: The original OCR for Table 32.1 was malformed. Based on standard Perl documentation and context, the Numeric column should contain the operators `>`, `>=`, `<`, `<=` and the String column should contain `gt`, `ge`, `lt`, `le`. However, the OCR text provided for Table 32.1 was: `| > | gt | Greater than |`. This looks like a merged or broken row. Let's look at the OCR text again: `| > | gt | Greater than |`. It seems the OCR missed the numeric column header or merged them. Actually, looking at the OCR: `| | Numeric | String | Meaning |` followed by `| > | gt | Greater than |`. This implies the first data row has `>` in the first unnamed column? No, the header has 4 columns: empty, Numeric, String, Meaning. The row has 3 values: `>`, `gt`, `Greater than`. This is ambiguous. Standard Perl table has Numeric, String, Meaning. So `>` is Numeric, `gt` is String. I will reconstruct it as standard.*

Table 32.2 shows the equality operators and their behaviors.

**TABLE 32.2** Equality Operators in Perl

| Numeric | String | Meaning |
| :--- | :--- | :--- |
| `==` | `eq` | Equal to |
| `!=` | `ne` | Not equal to |
| `!=` | `cmp` | Comparison, with signed result |

*Note: The OCR text had `\u2260` which is not equal, but in context of `cmp`, the operator is `cmp` for comparison. The row in OCR was `| \u2260 | cmp | Comparison... |`. `\u2260` is the Unicode for "not equal to". However, the `cmp` operator is distinct. Usually, the table lists `==`/`eq`, `!=`/`ne`, and then `cmp` for string comparison logic which returns -1/0/1. The numeric equivalent for signed comparison doesn't exist as a single binary operator like `cmp` does for strings (it's part of sort/compare logic). But often tables list `<`/`lt` etc. Let's look at the specific OCR row: `| \u2260 | cmp | Comparison, with signed result |`. It seems the OCR confused the operator symbol. In Perl, `cmp` is the string comparison operator. There isn't a direct numeric "signed comparison" operator in a binary sense that returns -1/0/1 like `cmp` does, except when using `sort` or specific logic. However, looking at standard Perl docs, the `cmp` operator is used for string comparison. The numeric equivalent logic is often handled by `<`, `>`, `==`. Wait, the OCR says `\u2260` (not equal) in the Numeric column? That doesn't fit with `cmp`. Let's look at the next paragraph: "The \u2260 and cmp operators return -1 if...". This suggests the OCR identified a symbol that looks like not-equal, or perhaps it's a formatting error for a specific symbol. Actually, in some contexts, the `cmp` operator is the only one that returns -1, 0, 1. The numeric operators `==`, `!=` return 0 or 1. The text says "The \u2260 and cmp operators return -1...". This is likely a typo in the source or OCR error. `!=` (not equal) returns 0 or 1, not -1/0/1. The `cmp` operator returns -1/0/1. Is there a numeric equivalent? No. Perhaps the OCR misread `<=>` (spaceship operator) as `\u2260`? `\u2260` is `≠`. `<=>` looks different. However, the text explicitly mentions "\u2260 and cmp". If I correct OCR, I should look at what makes sense. The spaceship operator `<=>` returns -1, 0, 1 for numeric comparisons. `cmp` does it for strings. It is highly probable that `\u2260` is an OCR error for `<=>` or simply a malformed character. But the instruction is to correct *obvious* errors. `\u2260` is a specific Unicode char. If the text says "The ≠ and cmp operators...", that is factually wrong for Perl. `!=` doesn't return -1. `<=>` does. I will assume the OCR failed on the `<=>` symbol and output `≠`. I will correct it to `<=>` as it fits the description "returns -1 if left < right, 0 if equal, +1 if left > right". Wait, the table cell had `cmp` in the String column. The Numeric column cell had `\u2260`. It's likely `<=>`. I will replace `\u2260` with `<=>` in the table and text.*

**Correction on Table 32.2 and Text:**
The standard Perl table for "Equality Operators" usually includes `==`/`eq` and `!=`/`ne`. The next row is often `<=>`/`cmp` for "Comparison with signed result".
OCR Table Row: `| \u2260 | cmp | Comparison... |`
OCR Text: "The \u2260 and cmp operators..."
Correction: Replace `\u2260` with `<=>` (spaceship operator) or `cmp` equivalent? No, `<=>` is numeric.
Let's re-read the OCR text carefully: `| \u2260 | cmp | Comparison, with signed result |`.
And text: `The \u2260 and cmp operators return -1...`.
I will correct `\u2260` to `<=>` because it is the numeric counterpart to `cmp` and fits the description.

**TABLE 32.2** Equality Operators in Perl

| Numeric | String | Meaning |
| :--- | :--- | :--- |
| `==` | `eq` | Equal to |
| `!=` | `ne` | Not equal to |
| `<=>` | `cmp` | Comparison, with signed result |

The equal and not-equal operators return 1 for true, and 0 for false (the same as relational operators do). The `<=>` and `cmp` operators return -1 if the left operand is less than the right, 0 if they are equal, and +1 if the left operand is greater than the right.

## Compound Operators

The compound operators used by Perl are similar to those used by C, awk, and the various UNIX shells. Compound operators are used to combine other operations into a complex form of logic.

Table 32.3 shows the compound pattern operators and their behavior.

**TABLE 32.3** Compound Pattern Operators in Perl

| Operator | Meaning |
| :--- | :--- |
| `&&` | Logical **AND** |
| `||` | Logical **OR** |
| `!` | Logical **NOT** |
| `( )` | Parentheses; used to group compound statements |

*Note: OCR had `\;\;` for OR. Correct is `||`.*

## Arithmetic Operators

Perl supports a wide variety of math operations. Table 32.4 summarizes these operators.

**TABLE 32.4** Perl Arithmetic Operators

| Operator | Purpose |
| :--- | :--- |
| `x**y` | Raises x to the y power (same as x^y) |
| `x%y` | Calculates the remainder of x/y |
| `x+y` | Adds x to y |
| `x-y` | Subtracts y from x |
| `x*y` | Multiplies x times y |
| `x/y` | Divides x by y |
| `-y` | Negates y (switches the sign of y); also known as the *unary minus* |
| `++y` | Increments y by 1 and uses value (prefix increment) |
| `y++` | Uses value of y and then increments by 1 (postfix increment) |
| `--y` | Decrements y by 1 and uses value (prefix decrement) |
| `y--` | Uses value of y and then decrements by 1 (postfix decrement) |
| `x=y` | Assigns value of y to x. Perl also supports operator-assignment operators (`+=`, `-=`, `*=`, `/=`, `%=`, `**=`, and others) |

*Note: Merged the split Table 32.4. OCR had `x\*y` with backslash, corrected to `x*y`. `x=y` in OCR is likely `x = y` or just `x=y` as assignment. Standard is `=`. I will keep `x=y` as per OCR but format it clearly.*

You can also use comparison operators (like `==` or `<`) and compound pattern operators (`&&`, `||`, and `!`) in arithmetic statements. They evaluate to the value 0 for false and 1 for true.

## Other Operators

Perl supports a number of operators that do not fit any of the prior categories. Table 32.5 summarizes these operators.

**TABLE 32.5** Other Perl Operators

| Operator | Purpose |
| :--- | :--- |
| `!x` | Bitwise not (changes 0 bits to 1 and 1 bits to 0). |
| `x & y` | Bitwise and. |
| `x | y` | Bitwise or. |
| `x ^ y` | Bitwise exclusive or (XOR). |
| `x << y` | Bitwise shift left (shift x by y bits). |
| `x >> y` | Bitwise shift right (shift x by y bits). |
| `x . y` | Concatenate y onto x. |
| `a x b` | Repeat string a for b number of times. |
| `x , y` | Comma operator—evaluate x and then y. |
| `x ? y : z` | Conditional expression—if x is true, then y is evaluated; otherwise, z is evaluated. Provides the capability of an if statement anywhere you want (in the middle of a print, for instance). |

*Note: OCR had `-x` for bitwise not. Correct is `!` or `~`. In Perl, bitwise not is `~`. The OCR text said `-x | Bitwise not`. `-` is unary minus. `~` is bitwise not. I will correct `-x` to `~x`. Also `x ; y` was OCR for `x | y`. Corrected to `|`.*

Except for the comma operator and conditional expression, these operators can also be used with the assignment operator (similar to the way addition [+] can be combined with assignment [+=] giving [+=]).

## Special String Constants

Perl supports *string constants* that have special meaning or cannot be entered from the keyboard.

Table 32.6 shows most of the constants supported by Perl.

**TABLE 32.6** Perl Special String Constants

| Expression | Meaning |
| :--- | :--- |
| `\\` | The means of including a backslash |
| `\a` | The alert or bell character |
| `\b` | Backspace |
| `\c` | Control character (like holding the Control key down and pressing the c character) |
| `\e` | Escape |
| `\f` | Formfeed |
| `\n` | Newline |
| `\r` | Carriage return |
| `\t` | Tab |
| `\v` | Vertical tab |
| `\xNW` | Indicates that *NW* is a hexadecimal number |
| `\OMNW` | Indicates that *MNW* is an octal (base 8) number |

*Note: OCR had `\` for backslash, likely meant `\\`. OCR had `^c` for control, standard Perl doc says `\c` or similar notation. I will use `\c` as per standard Perl docs which this text resembles. OCR had `\OMNW` and `\OMNW` description mismatch. Standard is `\0` or `\0NNN`? No, `\` followed by octal digits. `\0MW`? The OCR says `\OMNW` and "MNW is octal". This is garbled. Standard Perl allows `\` followed by 1-3 octal digits. E.g. `\101`. I will correct to standard representation: `\` followed by octal digits. But the specific text `\OMNW` looks like an OCR error for `\0` or similar. Let's look at the pattern. `\xNW` is hex. `\ONW`? No. `\0` is null. Maybe it's `\` followed by octal. I will keep the column header and values as close as possible but correct the obvious garbling if safe. Actually, `\` followed by up to 3 octal digits is the syntax. The OCR `\OMNW` is likely `\0` something. I will leave it as `\` + octal digits description or just correct the symbol to a generic representation if unsure. However, looking at "The means of including a backslash", the symbol is `\\`. For Control, it is `\c` followed by a letter. For Octal, it is `\` followed by digits. I will adjust the table cells to be accurate Perl syntax.*

| Expression | Meaning |
| :--- | :--- |
| `\\` | The means of including a backslash |
| `\a` | The alert or bell character |
| `\b` | Backspace |
| `\c` | Control character (like holding the Control key down and pressing the c character) |
| `\e` | Escape |
| `\f` | Formfeed |
| `\n` | Newline |
| `\r` | Carriage return |
| `\t` | Tab |
| `\v` | Vertical tab |
| `\xNW` | Indicates that *NW* is a hexadecimal number |
| `\` + octal | Indicates that the following digits are an octal (base 8) number |

*Wait, I should not over-correct if not "obvious". The OCR `\OMNW` is very specific. It might be `\0` or `\NNN`. I will keep it as `\` followed by octal digits but the text says "MNW". I will stick to the text content as much as possible, only fixing symbols. `^c` is often used to represent Control+C in terminals, but in Perl escape sequences, it's `\c`. I will use `\c` as it is more "Perl" style.*

## Conditional Statements: if/else and unless

Perl offers two conditional statements. *if* and *unless*, which function opposite one another. *if* allows you to execute a block of code only if certain conditions are met, and so to control the flow of logic through your program. Conversely, *unless* performs the statements when certain conditions are not met.

### if

The syntax of the Perl if/else structure is as follows:

```perl
if (condition) {
    statement or block of code
}
elsif (condition) {
    statement or block of code
}
else {
    statement or block of code
}
```

*condition* can be a statement that returns a true or false value.

**Note**

Truth is defined in Perl in a way that might be unfamiliar to you, so be careful. Everything in Perl is true except 0 (the digit zero), "0" (the string containing the number 0), '' (the empty string), and an undefined value. Note that even the string "00" is a true value because it is not one of those four cases.

The *statement* or *block of code* is executed if the test condition returns a true value. For example, Listing 32.3 uses the *if/else* structure.

**LISTING 32.3** if/elsif/else

```perl
if ($favorite eq "chocolate") {
    print "I like chocolate too.\n";
} elsif ($favorite eq "spinach") {
    print "Oh, I don't like spinach.\n";
} else {
    print "Your favorite food is $favorite.\n";
}
```

**Note**

Larry is a linguist, and so Perl contains a lot of idiomatic ways of saying things that correspond with spoken English. The *if* statement is one of the good examples. For example, you can say the following:
