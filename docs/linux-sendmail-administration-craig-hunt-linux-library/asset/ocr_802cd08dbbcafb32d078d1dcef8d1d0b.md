mail always goes through the same mailer, because only the recipient address is used to select the mailer.

The /try command ends by displaying a return code (Rcode) and the final address after processing is complete. A return code of zero means that everything went okay. A nonzero return code means that a potential delivery problem was encountered. Running an address that produces a non-zero return code through /parse will produce an error message describing the return code, as we saw earlier.

I find that I /try much more often than I /parse. Most of the configurations I work with a limited number of mailers, usually just smtp for all external mail and local for internal mail. I usually know what mailer will handle the mail without asking Mailsend. The /parse command is most useful when you use the mailer that you have several different mailers. A great time to use /parse is when you have a mailtable. For a complex configuration, the /parse command tells you the mailer that Mailsend will use and then processes the recipient address for that mailer. You can then process the sender address with /try.

# Displaying and Setting Internal Values

The tests in listings 10.8, 10.9, and 10.10 all show test mode being used to process an address through some rules. Address test mode can also be used to examine the contents of sendmail.cf variables and classes, to query for other types of runtime information, and even to set values to see how they affect the operation of the system, which is exactly what is done in Listing 10.11.

# Listing 10.11 Setting and Viewing Variables and Classes

```
> Sm
>/try smtp craig@wren.foobirds.org
Trying header sender address craig@wren.foobirds.org for mailer smtp
canonify input: craig @ wren . foobirds . org
... Many lines deleted ...
final
returns: craig @ wren . foobirds . org
Rcode = 0, addr = craig@wren.foobirds.org
>.Dfobirds.org
> Sm
foobirds.org
>/try smtp craig@wren.foobirds.org
Trying header sender address craig@wren.foobirds.org for mailer smtp
canonify input: craig @ wren . foobirds . org
... Many lines deleted ...
```