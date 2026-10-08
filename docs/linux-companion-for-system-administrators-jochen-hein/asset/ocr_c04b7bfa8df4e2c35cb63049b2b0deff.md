# NAMES OF LOCALES 233

| Locale | Language | Country | Character set |
| de_DE.646 | German | Germany | ISO 646 |
| de_DE.88591 | German | Germany | ISO-8859-1 |
| de_CH.88591 | German | Switzerland | ISO-8859-1 |
| de_AU.88591 | German | Austria | ISO-8859-1 |
| en_US.88591 | English | USA | ISO-8859-1 |
| en_UK.88591 | English | United Kingdom | ISO-8859-1 |
| C | English | Standard locale | US-ASCII |
| POSIX | English | Equivalent to C | US-ASCII |

**Table 8.1** Examples of locale names.

The language consists of two lower case characters. The abbreviations of the individual languages are defined in ISO 639.

The country consists of two upper case characters. The abbreviations of the individual countries are defined in ISO 3166.

The charset describes a character coding standard. If this field contains only digits, it stands for the number of the corresponding ISO standard. If no character set is specified, it can be safely assumed to be ISO-8859-1¹. If it is not possible to describe the standard with digits alone, only additional lower case letters should be used, and no separators such as dot (.) or comma (,). If only one character set is used in a country, this field may be omitted.

1. The ISO 8859-1 character set was defined about 12 years ago; NLS was introduced, by AT&T for example, in the late 1980s and early 1990s with System V(TR386) Release 4; and MIME as an 8-bit clean news and mail coding/decoding software became a standard as early as 1992. This should be a sufficient transition time to stop assuming that US-ASCII is still used as a default – do our football league reporters go on talking about dark and light shorts because you might still own a black and white gobble?