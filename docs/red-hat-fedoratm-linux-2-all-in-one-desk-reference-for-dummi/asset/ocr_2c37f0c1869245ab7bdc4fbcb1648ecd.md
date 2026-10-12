+   1. Use a text editor to type and save the following script in a file named lookup:
+   ```perl
+   #!/usr/bin/perl
+   while (STDIN) {
+       if ($_ =~ /[bB]laster/ ) { print $_; }
+   }
+   ```
+   2. Make the lookup file executable by using the following command:
+   `chmod +x lookup`
+   3. Try the script by using the following command:
+   `cat /usr/src/linux*/drivers/cdrom/sbpdc.c | ./lookup`

In this case, the cat command feeds the contents of a specific file (which, as you know from the grep example, contains some lines with the regular expression) to the lookup script. The script simply applies Perl’s regular expression–match operator (=~) and prints any matching line. The output is similar to what the grep command displays with the following command:
`grep "[bB]laster" /usr/src/linux*/drivers/cdrom/sbpdc.c`

The $_ variable in the lookup script needs some explanation. The <STDIN> expression gets a line from the standard input and, by default, stores that line in the $_ variable. Inside the while loop, the regular expression is matched against the $_ string. The following single Perl statement completes the lookup script’s work:
`if ( $_ == /[bB]laster/ ) { print $_; }`

This example illustrates how you might use a regular expression to search for occurrences of strings in a file.

After you use regular expressions for a while, you can better appreciate their power. The trick is to find the regular expression that performs the task you want. For example, here is a search that looks for all lines that begin with exactly seven spaces and end with a closing parenthesis:

```perl
while (STDIN) {
    if ( $_ == /^\s\s\s\s\s\s\s\) $ ) { print $_; }
}
```

# Flow-control statements

So far, you have seen Perl statements intended to execute in a serial fashion, one after another. Perl also includes statements that enable you to control