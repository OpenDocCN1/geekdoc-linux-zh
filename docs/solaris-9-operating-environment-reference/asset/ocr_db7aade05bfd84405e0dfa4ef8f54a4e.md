# dumpcs 283

With one or more numeric options specified, dumpcs shows EUC charset(s) for the current locale according to the numbers specified and in order of charset number. Each nonprintable character is represented by an asterisk (*) and enough ASCII space character(s) to fill that charset's column width.

> Note — dumpcs can handle only EUC locales.

# Options

+   -0 ASCII (or EUC primary) coderset.
-1 EUCIPSET 1 if used for the current locale.
-2 EUCIPSET 2 if used for the current locale.
-3 EUCIPSET 3 if used for the current locale.

Verbose, ranges of nonprintable characters are collapsed into a single line. This option produces one line for each nonprintable character.

Replace code values with corresponding wide character values (values).

# Examples

The following example first uses the dumpcs command with no arguments, then uses the -0 option. Notice that the output from these two commands is identical.

```
castle% dumpcs
::::::::
LC_CTYPE:C CS:0
::::::::
20  !" # $S% & ' ( ) * +, . / 0 1 2 3 4 5 6 7 8 9 ; <= > =
40  @ A C D E F G H I J K L M N O P Q R S T U V W X Y Z [ ] ^ -
60  a b c d e f g h i j k l m n o p q r s u v w x y z ( | ) * -
```

```
::::::::
LC_CTYPE:C CS:1
*
20  !" # $S% & ' ( ) * +, . / 0 1 2 3 4 5 6 7 8 9 ; <= > =
40  @ A C D E F G H I J K L M N O P Q R S T U V W X Y Z [ ] ^ -
60  a b c d e f g h i j k l m n o p q r s u v w x y z ( | ) * -
```

```
castle% dumpcs -1
::::::::
LC_CTYPE:C CS:1
*
castle%
```

# Environment Variables

The environment variables LC_CTYPE and LANG control the character classification throughout dumpcs. On entry to dumpcs, these environment variables are checked in