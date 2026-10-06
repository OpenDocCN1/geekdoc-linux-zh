# Options That Control Filename Pattern Matching (Continued)

GLOB_DOTS

Normally, to match a filename beginning with a period (.), you have to give the period explicitly in the pattern (none of the special characters match a leading period in a filename). Setting this option causes special characters to match leading periods. The filenames and . must always be given explicitly because no pattern matches them.

# Pattern Matching Special Characters

+   * Matches any string of characters, including the null string (example, a string containing no characters at all).

+   * [...] Matches any one of the characters enclosed in the brackets (for example, [abc] matches either a, b, or c). You can separate the first and last characters in a sequence with a hyphen (-), [a-z] matches any lowercase letter, [0-9] matches any digit, and [A-Za-z] matches any upper or lowercase letter. If the string within the brackets begins with a caret (^), it matches any single character except those inside the brackets.

+   * <x-y> Matches any number from x to y (for example, <10-15> matches 10, 11, 12, 13, 14, and 15). As special cases <-y> matches any less than y, <-> matches any number greater than x, and <-> (or just <) matches any number at all.

+   * ^ Any pattern can be enclosed in parentheses.

+   * Matches any filename that is not matched by the pattern x (for example, *.c matches all filenames that do not end in .c). The Shell applies ^ before matching a /, ^top/level1 looks for filenames named level2 in all the subdirectories of the working directory except for the subdirectory top.

+   * Matches anything matched by pattern x or by pattern y, *(tree).c matches all filenames ending in either tree.c or code.c. The | must always be enclosed in parentheses so that the shell does not treat it as a pipe symbol.