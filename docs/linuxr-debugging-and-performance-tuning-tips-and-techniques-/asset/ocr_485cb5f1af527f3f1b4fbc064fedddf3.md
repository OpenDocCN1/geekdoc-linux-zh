```
while (fgets(buf, sizeof buf, stdin) != NULL) {
local[e0] = '0';
count = sscanf(buf, "%s %s", left, right, locale);
if (count < 2)
break;

if (*locale)
setlocale(LC_ALL, locale);
strcpy(curloc, locale);
}

printf("%s: strcmp(\"%s\", \"%s\") is %d\n", curl oc, left,
right, strcmp(left, right));
printf("%s: strol1(\"%s\", \"%s\") is %d\n", curl oc, left,
right, strol1(left, right));

printf("\n--> ");
fflush(stdout);
}

exit(0);
)
```

The program reads input lines, which consist of two words to compare and, optionally, a locale to use for the comparison. If the locale is given, that becomes the locale for subsequent entries. It starts out with whatever locale is set in the environment.

The `curloc` array saves the current locale for printing results; `left` and `right` are the left- and right-hand words to compare (lines 10–11). The main part of the program is a loop (lines 19–36) that reads lines and does the work. Lines 20–23 split up the input line. `locale` is initialized to the empty string, in case a third value isn’t provided.

Lines 25–28 set the new locale if there is one. Lines 30–33 print the comparison results, and line 35 prompts for more input. Here’s a demonstration:

```
$ ch13-compare
--> ABC abc
C: strcmp("ABC", "abc") is -1
C: strol1("ABC", "abc") is -1
```

Run the program
Enter two words
Program started in “C” locale
strcmp() results don’t change
Identical results in “C” locale

```
--> ABC abc en_US
en_US: strcmp("ABC", "abc") is -1
en_US: strol1("ABC", "abc") is 2
```

Same words, “en_US” locale
Same results don’t change
strol1() results do!

```
--> ABC abc en_US.UTF-8
en_US.UTF-8: strcmp("ABC", "abc") is -1
en_US.UTF-8: strol1("ABC", "abc") is 6
```

Same words, “en_US.UTF-8” locale
Different value, still positive

```
--> junk JUNK
en_US.UTF-8: strcmp("junk", "JUNK") is 1
en_US.UTF-8: strol1("junk", "JUNK") is -6
```

New words
Previous locale used