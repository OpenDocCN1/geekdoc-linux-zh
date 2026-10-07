The headers in Listing 7.11 provide examples of using the conditional syntax in header
templates. The conditional syntax is an if/else construct $? is the "if," $| is the
else," and is the "endif." This is exactly the same conditional syntax that was
described for the D command, and it is used in the same way. An example from
Listing 7.11 is:

```
H?F?Resent-From: $?$x $<g|$g$.
```

H is the command. ?F is a flag value. Resent-From: is the header name, and ?$x
$<g>|$ is the template, which uses conditional syntax. This conditional template
says that if (?) macro exists, use Sx $<g> as the header template, else ($) us as
the template. Marco contains the full name of the sender. Thus, if it exists, the header is

Resent-From: David Craig david@wren.foobirds.org

If x doesn't exist, the header is

Resent-From: david@wren.foobirds.org

The headers provided in the Linux sendmail.cf are sufficient for a basic installation.
You'll see additional header declarations in Chapter 11, "Stopping Spam," for mail fil-
tering, but the basic declarations shown in Listing 7.11 will be found on all systems.

All five sections discussed so far—Local Info, Options, Message Precedence, Trusted
Users and Format of Headers—define configuration values used by Sendmail. These sec-
tions are essentially passive, telling Sendmail things such as the structure of headers or the
locations of files. These sections have not defined the actions that Sendmail should take.
With changes with the next section. The Rewrite Rules section contains the instructions
that Sendmail uses to process mail.

# # Rewriting Rules Section

The Rewriting Rules defines the rules used to parse e-mail addresses from user
mail programs and rewrite them into the form required by the mail delivery programs.
Rewrite rules match the input address against a pattern, and if a match is found, rewrite
the address in a new format using the rules defined in the command. The format of a
rewrite rule is:

```
Rpattern     template
```

where R is the command. pattern selects the address to be modified and template
rewrites the address.