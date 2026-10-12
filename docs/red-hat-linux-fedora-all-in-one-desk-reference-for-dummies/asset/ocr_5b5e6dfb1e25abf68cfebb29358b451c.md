( !~ ) operators to test a string. You can write a Perl script that performs the same search as the one done with grep earlier in this section. Follow these steps to complete this task:

1. Use a text editor to type and save the following script in a file named lookup:

```
#!/usr/bin/perl

while (<STDIN>)
{
    if ( $_ =~ /[bB]laster/ ) { print $_; }
}
```

2. Make the lookup file executable by using the following command:

```
chmod +x lookup
```

3. Try the script by using the following command:

```
cat /usr/src/linux*/drivers/cdrom/sbpcd.c | ./lookup
```

In this case, the cat command feeds the contents of a specific file (which, as you know from the grep example, contains some lines with the regular expression) to the lookup script. The script simply applies Perl's regular expression-match operator (=~) and prints any matching line. The output should be similar to what the grep command displays with the following command:

```
grep "[bB]laster" /usr/src/linux*/drivers/cdrom/sbpcd.c
```

The $_ variable in the lookup script needs some explanation. The <STDIN> expression gets a line from the standard input and, by default, stores that line in the $_ variable. Inside the while loop, the regular expression is matched against the $_ string. The following single Perl statement completes the lookup script's work:

```
if ( $_ =~ /[bB]laster/ ) { print $_; }
```