```
`push(@strArray, ucfirst($str));`
`}`
`my $formattedName = join(' ', @strArray);`
```

Where the $name variable is processed. The first line uses Perl's built-in lc() function, which lowercases a given string. Because lc() is given the $name string as the parameter, it returns a lowercase value of the name, which we store back in the name variable $name. We lowercase the name so that we can uppercase only the first letter of each name. Now a user named Carol Godsave might enter many different combinations of her name. For example:

+   * Carol Godsave
+   * CAROL GODSAVE
+   * carol godsave
+   * carol GODSAVE
+   * cAROL GoDSave
+   * carol GoDsAvE

As you can see the user can enter one of these or many other combinations of letters to represent her name. However, we would want to display “Carol Godsave” since because that's the proper formatting for her name. So our processing code block uses the following algorithm:

+   1. Lower case the name. This effectively turns whatever Carol entered for her name into `carol godsave`.
+   2. Split each word separated by a space character. This gives us `carol` and `godsave`.
+   3. Uppercase only the first letter of each part. This gives us `Carol` and `Godsave`.
+   4. Put together the parts by separating them with a space character. This returns `Carol Godsave`, which is exactly what we want.

In this code segment we use an array called @strArray, which we initialize to empty the list. Then a foreach loop is used to cycle through the each part of the name that is split using the split() function found in Perl. The split() is called with two parameters: separator, which in this case is a white space character written in regular expression format `/ /`, and the string that needs to be separated, which in this case is $name. The split() function returns the separated parts in an array. So, effectively, in Carol's case the foreach loop looks like:

```
`foreach my $str ('carol', 'godsave') {`
`    push(@strArray, ucfirst($str));`
`}`
```

The loop cycles through each part and uppercases only the first character of each part using the built-in ucfirst() function call. When ucfirst() is given a string parameter, it uppercases only the first character and returns the modified string. For example ucfirst('carol') will return `Carol`; similarly, ucfirst('godsave')