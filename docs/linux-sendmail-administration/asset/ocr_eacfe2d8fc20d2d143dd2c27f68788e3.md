The last line in Listing 7.3 is C{src}E F H U. It defines essentially the same thing as the two commands described above. It defines a long class variable name, {src}, and it assigns a list of values to that class that are used in the Sendmail syntax. In this case, the values are internally assigned by Sendmail to addresses it is in processing. What is unique about this C command is that it occurs outside of the Local Info section. This illustrates the fact that, while most variables declared in the Local Info section, they can be declared anywhere in the sendmail.cf file as long as they are declared before they are used. This C command occurs immediately before the outset that uses it. On the other hand, all F commands in our sample sendmail.cf file are located in the Local Info section.

# Loading a Class Variable from a File

The F command loads values into a class variable from a file. The Local Info section from the sample sendmail.cf file contains only two commands, which are shown in Listing 7.5.

# Listing 7.5 Commands that Load Variables from a File

```
[root]# grep 'F' /etc/sendmail.cf
FW/etc/mail/local-host-names
FR-o /etc/mail/relay-domains
```

The first F command is the simplest form of the syntax—the F command followed by the variable name, in this case w, and the path of the file that is be loaded into the variable, in this case is /etc/mail/local-host-names. This simple form of the F command is the most commonly used, but it is not the only format. The F command accepts an optional switch value before the path of the file and an optional scanf pattern after the file path.

By default, Sendmail reads data from the file using the scanf %s, which means it reads the first whitespace-delimited string from each line in the file. A different scanf pattern can be provided on the F command if Sendmail is compiled with the SCANF compiler option. We saw from the sendmail -bt -d0.4 command in Listing 7.6 in Chapter 6 that the copy of Sendmail delivered with the Red Hat RPM uses the SCANF option. Therefore, we could enter a command in the following format if we needed to:

```
FW/etc/mail/local-host-names %.25s
```

This command reads data from local-host-names into class w but it reads more than 25 characters from a string if a whitespace character has not been encountered. Why would you do this? You wouldn't. This is just an example of the possible syntax. I never use a scanf pattern with the F command, and neither should you expect