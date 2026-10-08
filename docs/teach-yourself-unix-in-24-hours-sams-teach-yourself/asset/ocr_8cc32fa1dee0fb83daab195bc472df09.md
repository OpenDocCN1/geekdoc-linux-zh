# Getting onto the System and Using the Command Line

4. My favorite example of the cat program is to ask for the year 1752, the year when the Western calendar switched from Gregorian to Julian. Particularly the month of September, during which the switch actually occurred.

% cat 1752

| Jan S M Tu W Th F S | Feb S M Tu W Th F S | Mar S M Tu W Th F S |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---||
| | | 1 2 3 4 | | 1 | | 1 2 3 4 5 6 7 |
| 5 6 7 8 9 10 11 | 2 3 4 5 6 7 8 | 8 9 10 11 12 13 14 |
| 12 13 14 15 16 17 18 | 9 10 11 12 13 14 15 | 15 16 17 18 19 20 21 |
| 19 20 21 22 23 24 25 | 16 17 18 19 20 21 22 | 22 23 24 25 26 27 28 |
| 26 27 28 29 30 31 | 23 24 25 26 27 28 29 | 29 30 31 |

| Apr S M Tu W Th F S | Jun S M Tu W Th F S | Jul S M Tu W Th F S |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---||
| | | | | | | 1 | | | | | | | 2 | 1 2 3 4 5 6 |
| 5 6 7 8 9 10 11 | 2 3 4 5 6 7 8 | 5 6 7 8 9 10 11 |
| 12 13 14 15 16 17 18 | 9 10 11 12 13 14 15 | 12 13 14 15 16 17 18 |
| 19 20 21 22 23 24 25 | 16 17 18 19 20 21 22 | 19 20 21 22 23 24 25 |
| 26 27 28 29 30 31 | 23 24 25 26 27 28 29 | 26 27 28 29 30 31 |

| Oct S M Tu W Th F S | Aug S M Tu W Th F S | Sep S M Tu W Th F S |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---||\|
| | | | 1 2 3 4 | | | | | | | 1 2 3 4 5 6 |
| 8 9 10 11 12 13 14 | 2 3 4 5 6 7 8 | 7 8 9 10 11 12 13 |
| 15 16 17 18 19 20 21 | 9 10 11 12 13 14 15 | 14 15 16 17 18 19 20 |
| 22 23 24 25 26 27 28 | 16 17 18 19 20 21 22 | 21 22 23 24 25 26 27 |
| 29 30 31 | 23 24 25 26 27 28 29 | 28 29 30 |

| Nov S M Tu W Th F S | Oct S M Tu W Th F S | Dec S M Tu W Th F S |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---||\|
| | | | | 1 2 3 4 | | | | | | | 1 2 |
| | | | | 5 6 7 8 9 | 8 9 10 11 12 13 14 | 3 4 5 6 7 8 9 |
| 10 11 12 13 14 15 16 | 15 16 17 18 19 20 21 | 10 11 12 13 14 15 16 |
| 17 18 19 20 21 22 23 | 22 23 24 25 26 27 28 | 17 18 19 20 21 22 23 |
| 24 25 26 27 28 29 30 | 29 30 31 | 24 25 26 27 28 29 30 |
| 31 | |

%

You can experiment with cat and easily find out information—for example, what day of the year your parents were born. If you're curious about whether Christmas 1999 was on a weekend, can cat answer that?

When you used cat, you entered the name of the command and some additional information to get the exact action you desired. You tried both cat 10 and 93, and cat 10 1993. In UNIX parl, the path is the first command, and the subsequent words are arguments or options to use. A special class of options are that begin with a single dash, flags, and you will learn about those that are in the next