
# NAMES OF LOCALES 233

| Locale | Language | Country | Character set |
| :--- | :--- | :--- | :--- |
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

# 234 NATIONAL LANGUAGE SUPPORT

## 8.4 Categories used in NLS

This section presents a brief description of the different categories of a locale which are shown in Table 8.2. The names used for the individual categories are the names of the corresponding environment variables.

| Variable | Description |
| :--- | :--- |
| LC_COLLATE | Sorting order of characters and character strings |
| LC_CTYPE | Assignment of characters to character classes |
| LC_MESSAGES | Language for messages and man pages |
| LC_MONETARY | Information on formatting of amounts of currency |
| LC_NUMERIC | Formatting of numbers |
| LC_RESPONSE | Language for responses |
| LC_TIME | Formatting of date and time |

**Table 8.2** Overview of locale categories.

### 8.4.1 The LC MESSAGES category

The language of message texts of individual programs and the messages from the C library is defined by the environment variable LC_MESSAGES. This category has been implemented in the LINUX C library libc since version 4.5.26.

A change of this category has almost immediate consequences for the user, because it significantly changes the behaviour of the system, which now interacts with the user in the specified language instead of standard English.

Message texts are no longer directly output by the programs, but are read from a message catalog. On the basis of the values assigned to the variables LANG (LC_MESSAGES or LC_ALL), the corresponding catalog is opened and the messages are extracted. If no message catalog is present, the messages are output in the default language (English). The messages in the default language are still present directly in the program, so no message catalog is needed if the default language of a program is to be used.

Translation of the message texts of a program into another language does not require recompilation of the program. Even, the same program can be used on one system by different users in different languages if the appropriate message catalog exists for each of these languages.

The process of reading messages from message catalogs is not part of the ANSI-C or POSIX standards. Therefore, LINUX uses the standard proposed by X/Open. The creation of a message catalog is briefly described in Section 8.6.

# CATEGORIES USED IN NLS 235

With gettext, the GNU project uses a less complicated interface for the programmer to read messages from files at runtime. The package also includes a sophisticated Emacs mode for translation of messages.

Programs do not only output messages and text, but often require confirmation that such function is really to be executed. Such a question can be answered with 'yes' or 'no', or the equivalent in the selected language. Since there are different possibilities of answering (for example, 'yes', 'Yes', 'y', or 'Y'), the answer is internally handled by means of a regular expression. The program is responsible for checking whether the answer matches one of the regular expressions, as shown in Table 8.3.

| Language | Yes answer | No answer |
| :--- | :--- | :--- |
| C/POSIX | [yY][[:alpha:]] | [nN][[:alpha:]] |
| de_88591 | [jJ][[:alpha:]] | [nN][[:alpha:]] |
| fr_88591 | [oO][[:alpha:]] | [nN][[:alpha:]] |
| it_88591 | [sS][[:alpha:]] | [nN][[:alpha:]] |

**Table 8.3** Possible yes/no answer.

### 8.4.2 The LC_CTYPE category

The character set to be used is defined via the variable LC_CTYPE. In this category, the assignment of characters to character classes. This includes, for example, upper and lower letters and printable characters. Many programs, for example emacs, less, do not interpret the locale, but directly evaluate the value of LC_CTYPE. The default is ISO-8859-1 if the ISO-Latin-1 character set is be used. Also in the C library (libc) the locale ISO-8859-1 is hard-coded for the LC_TYPE, so no further description of this locale is needed.

### 8.4.3 The LC_COLLATE category (sorting order)

The sorting order for characters and character strings is set via the variable LC_COLLATE. In the standard locale, sorting is performed by ASCII code. This may sometimes be useful, because the procedure is very fast. However, ever, characters which need to be sorted together have completely different codes. In a phone book, for example, accented vowels and umlauts need to be sorted together with the corresponding plain vowels. Such behaviour can be obtained by creating the appropriate locale.

### 8.4.4 THE LC_TIME (date and time)

Another difference between countries (independently of whether they use the same language) is the format of date and time indications. The rules to be used are determined by the variable LC_TIME. In the USA, a date is usually indicated in the format MM/DD/YYYY, whereas in the United Kingdom DD/MM/YYYY is used. In Germany, for example, the template is DD.MM.YYYY. Thus, the date '9 June 1998' would be formatted in the different countries as shown in Table 8.4.

| Country | Formatted date |
| :--- | :--- |
| USA | 06/09/1998 |
| United Kingdom | 09/06/1998 |
| Germany | 09.06/1998 |

**Table 8.4** Formatted dates in different countries.

This category is also used to translate the names of days and months and the three-letter abbreviations as the selected language.
