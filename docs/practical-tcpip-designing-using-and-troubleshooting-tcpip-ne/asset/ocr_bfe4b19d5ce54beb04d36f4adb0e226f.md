# # Appendix 13 Base64 encoding

Base64 encoding lets you transform arbitrary 8-bit data into a series of printing characters without losing any information. This is used in e-mail and other applications to allow binary data to be transmitted safely over links that might not be able to handle binary data otherwise.

Here’s how Base64 works:

+   - split the input into chunks of three characters at a time (i.e. 24 bits)
+   - divide each 24-bit chunk into four pieces of 6 bits each. The number of different values that can be stored in 6 bits is 2^6 = 64 (hence Base64)
+   - look up each 6-bit value in the table below, and output the corresponding character. (In the table heading, I means “input”, O means “output”.)
+   - if the last input chunk consists of only one or two bytes (i.e. only 8 or 16 bits) it’s padded out with four or two 0-bits respectively, to make it up to a multiple of 6-bits, and the output is padded at the end with two or one “=” characters, respectively.

| I | O | I | O | I | O | I | O |
|---|---|---|---|---|---|---|---|
| 0 | A | 17 | R | 34 | i | 51 | z |
| 1 | B | 18 | S | 35 | j | 52 | 0 |
| 2 | C | 19 | T | 36 | k | 53 | 1 |
| 3 | D | 20 | U | 37 | l | 54 | 2 |
| 4 | E | 21 | V | 38 | m | 55 | 3 |
| 5 | F | 22 | W | 39 | n | 56 | 4 |
| 6 | G | 23 | X | 40 | o | 57 | 5 |
| 7 | H | 24 | Y | 41 | p | 58 | 6 |
| 8 | I | 25 | Z | 42 | q | 59 | 7 |
| 9 | J | 26 | a | 43 | r | 60 | 8 |
| 10 | K | 27 | b | 44 | s | 61 | 9 |
| 11 | L | 28 | c | 45 | t | 62 | + |
| 12 | M | 29 | d | 46 | u | 63 | / |
| 13 | N | 30 | e | 47 | v |  |  |
| 14 | O | 31 | f | 48 | w |  |  |
| 15 | P | 32 | g | 49 | x |  |  |
| 16 | Q | 33 | h | 50 | y |  |  |