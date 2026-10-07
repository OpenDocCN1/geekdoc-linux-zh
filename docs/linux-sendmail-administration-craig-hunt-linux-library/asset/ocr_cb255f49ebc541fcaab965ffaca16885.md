The last line in Listing 7.3 is C(src) E F H U. It does essentially the same thing as the two commands just described. It defines a long class variable name, {src}, and assigns a list of values to class that are used in the Sendmail syntax. In this case, the values are tagged internally by Sendmail to addresses to aid it in parsing the various types of addresses that can be found in the Sendmail databases. What is unique about this C command is that it occurs outside of the Local Info section. All of the other commands are found in the Local Info section. This illustrates the fact that, while most variables are declared in the Local Info section, they can be declared anywhere in the sendmail.cf file as long as they are declared before they are used. This command occurs immediately before the rule that uses it. On the other hand, all active F commands in our sample sendmail.cf file are located in the Local Info section.

# Loading a Class Variable from a File

The F command loads values into a class variable from a file. The Local Info section from the sample sendmail.cf contains only two F commands, which are shown in Listing 7.5.

# Listing 7.5 Commands that Load Variables from a File

```
[root] grep '^F' /etc/sendmail.cf
Fw/etc/mail/local-host-names
FR-0 /etc/mail/relay-domains
```

The first C is the simplest form of the syntax—the F command followed by the variable name, in this case w, and the pathname of the file to be loaded into the variable, which in this case is /etc/mail/local-host-names. This simple form of the F is the most commonly used, but it is not the only format. The command syntax accepts an optional switch value before the pathname of the file and an optional scf pattern after the pathname.

By default, Sendmail reads data from the file using the scanf pattern %s, which means it reads the first white space-delimited string from each line in the file. A different scf pattern can be provided on the F command if Sendmail is compiled with the SCANF compiler option. We saw from the sendmail -bt -d0.4 command in Listing 6.1 in Chapter 6 that the code of Sendmail delivered with the Red Hat RPM does use the SCANF compiler option. Therefore, we could enter a command in the following format if we needed:

```
Fw/etc/mail/local-host-names %25s
```

This command reads data from local-host-names into class w it reads no more than 25 characters from a string even if a whitespace character has not been encountered. Why would you do this? You wouldn't. This is just an example of the possible syntax. If you use a scanf pattern with the F command, and neither should you.