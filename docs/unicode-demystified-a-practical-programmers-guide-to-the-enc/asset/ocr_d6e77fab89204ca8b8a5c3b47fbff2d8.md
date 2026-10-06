# Case Conversion

The emacs editor can force words or Regions to all uppercase, lowercase, or initial caps (the first letter of each word uppercase, the rest lowercase). Refer to Table 11-15.

# Case Conversion || table 11-15

| META-I (lowercase "ill") | Converts word to the right of Point to lowercase |
| META-u | Converts word to the right of Point to uppercase |
| META-c | Converts word to the right of Point to initial caps |
| CONTROL-X-CONTROL-L | Converts Region between Point and Mark to lowercase |
| CONTROL-X-CONTROL-U | Converts Region between Point and Mark to uppercase |

The word-oriented conversions move Point over the word just converted, the same as META-I, allowing you to walk through text, converting each word with META-I-u, or META-c, and skipping words to be left alone with META-I. A positive numeric argument converts many words to the right of Point, moving Point as it goes. A negative numeric argument converts many words to the left of Point and leaves Point stationary. This is useful for quickly changing the case of words you have just typed. Some examples appear in Table 11-16.

| Characters and Commands Results || table 11-16 |
| HELLOMETA-META-I (lowercase "ill") | hello |
| helloMETA-META-u | HELLO |
| helloMETA-META-c | Hello |

The word conversions are not picky about beginning in the middle of a word. In all cases, they consider the first word-constituent character to the right of Point as the beginning of the word to be converted.

# Text Mode

With very few exceptions, the commands for human-language text units, such as words and sentences, are always turned on and available, even in the programming