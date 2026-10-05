enclose special addresses changes, values changed to be added to the . [ classes to handle these changes without changing the entire sendmail.cf file.

The second advantage of a class over a literal is the `$` syntax allows Sendmail to check for a “not equal” condition. A grep of the sample sendmail.cf in List 7.4 shows that, at least in the case of the [ class, this capability is important.

# Listing 7.4 Checking How Classes Are Used

```
[craig]$ grep \$1-" . /etc/sendmail.cf
[craig]$ grep \$1[' . /etc/sendmail.cf
[craig]$ grep \$1\" . /etc/sendmail.cf
[craig]$ grep \$1\' . /etc/sendmail.cf
R $ '[' : $* > $ $MailerToTriple < $1 : $2 > $3 check -- resolved?
R $ '$ '[' : $* > $ $MailerToTriple < $2 : $3 > $4 check -- resolved?
R $ '[' : $* > $ $MailerToTriple < $1 : $2 > $3 \." found?
```

Listing 7.4 shows many things. When used in the configuration, class variable must be referred as either `=$` or `$[. Using `grep` to search for these values shows how these variables are used. First off, class . is not used at all, and there are no tests using `=$` to see if a value exists in the [ class variable. However, `$` is used to select addresses that do not start with a [ . This is not the time to discuss the exact details of the pattern matching. Pattern matching is detailed in Chapter 8. The thing to understand here is that even inexplicable commands such as C[ might have a valid use.

> Remember that your system might be different. These class names may be used for other purposes on your system. This shows how they are used in our example sendmail.cf. Carefully read the comments in your sendmail.cf file for guidance on how classes and variables are used in your configuration.

The next two lines in List 7.3 are:

```
C(Accept)OK RELAY
C({tls})VERIFY ENCR
```

These two commands use long class variable names, (Accept) and {tls}, and both define keywords used to configure some aspect of Sendmail. You recognize the OK and RELAY keywords from the discussion of the access database in Chapter 6, “Using Sendmail Databases.\ You will see the VERIFY and ENCR keywords in the discussion of STARTTLS in Chapter 12, “Sendmail Security."