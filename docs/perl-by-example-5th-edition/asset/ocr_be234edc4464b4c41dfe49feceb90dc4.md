| | Per Syntax and Constructs (continued) |
| :--- | :--- |
| | **EXAMPLE**
use constant BUFFER_SIZE => 4096;
use constant Pi => 4 * atan2 1, 1;
use constant DBGLOGGING => 0;
use constant ISBN => "0-13-028251-0";
Pi+=6; # Cannot modify Pi; produces an error. |
| Numbers | Perl supports integers (decimal, octal, hexadecimal), floating-point numbers, scientific notation.

See Section 4.3.2, "Literals (Numeric, String, and Special)." |
| | **EXAMPLE**
$year = 2016; # integer
$mode = 0775; # octal number in base 8
$product_price = 29.95; # floating-point number in base 10
$favorite_color = 0x33CC99; # integer in base 16 (hexadecimal)
$distance_to_moon=3.844e5; # floating-point in scientific notation
$bits = 0b10110110; # binary number |
| Strings and Quotes | A string is a sequence of characters enclosed in quotes. The quotes must be matched; for example, 'string' or "string". Scalar and array variables ($x, @name) and backslash sequences (\n, \t, \v, etc.) are interpreted within double quotes; a backslash will escape a quotation mark. A single quote can be embedded in a set of double quotes; and a double quote can be embedded in a set of single quotes. A *here* document is a block of text embedded between user-defined tags; the first tag preceded by `<<`. The following shows three ways to quote a string:
Single quotes: 'It rains in Spain';
Double quotes: "It rains in Spain";
*here* document: print <<EOF;
    It rains in Spain
EOF
See Section 4.3.1, "Quotes Matter!" and Section 4.3.3, "Printing Without Quotes—The *here* document." |
| | **EXAMPLE**
Question = 'He asked her if she wouldn\'t mind going to Spain';
$answer = 'She said: "No, but it rains in Spain."';
$line = "\tHe said he wouldn't take her to Spain\n";
$temperature = '78';
print "It is currently $temperature degrees.";
# Prints: 'It is currently 78 degrees.' because variables are
# interpreted when enclosed in double quotes, but not single
print <<END;
    It
    rains in
    Spain
END
# Prints: "It rains in Spain" |