```
$ cat re11.pl
  $stg = "My name is Sam";
  $stg =~ s/My name is (.*)/$1/;
  print "Matched: $stg\n";

$ perl re11.pl
Matched: Sam
```

The next example uses regular expressions to parse a string for numbers. Two variables are initialized to hold a string that contains two numbers. The third line of the program uses a regular expression to isolate the first number in the string. The \D matches a string of zero or more characters that does not include a digit; The \d special character matches any single nondigit character. The trailing asterisk makes this part of the regular expression perform a greedy match that does not include a digit (it matches What is ). The bracketed regular expression \d+ matches a string of one or more digits. The parentheses do not affect what the regular expression matches; they allow the $1 in the replacement string to match what the bracketed regular expression matched. The final .* matches the rest of the string. This line assigns the value of the first number in the string to $string.

The next line is similar but assigns the second number in the string to $string2. The print statements display the numbers and the result of subtracting the second number from the first.

```
$ cat re8.pl
  $string = "What is 488 minus 78?";
  $string2 = $string;
  $string  =~ s/^\d*(\d+).*$/$1/;
  $string2 =~ s/\d*\d+\d*(\d+).*$/$1/;

  print "$string\n";
  print "$string2\n";
  print $string - $string2, "\n";

$ perl re8.pl
488
78
410
```

The next few programs show some of the pitfalls of using unquoted parentheses in regular expressions when you do not intend to bracket part of the regular expression. The first of these programs attempts to match parentheses in a string with unquoted parentheses in a regular expression, but fails. The regular expression ag( matches the same string as the regular expression ag\( because the parenthesis is a special character; the regular expression does not match the string ag(ed).

```
$ perl -le 'if ("ag(ed)") =~ /ag(ed)/ { print "true";} else {print "false";}'
false
```

The regular expression in the next example quotes the parentheses by preceding each with a backslash, causing Perl to interpret them as regular characters. The match is successful.