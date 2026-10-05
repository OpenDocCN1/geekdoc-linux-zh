# The sendmail configuration pieces

for a sendmail acting as an MSA. The flags with which sendmail is started determine which config file uses: -bm, -bs, and -bt use submit.cf if it exists, and all other modes use sendmail.cf. You can change these names with command-line flags or config options, but it is best not to.

The raw config file format was designed to easily parse by machines, not humans. The m4 source (.mc) file from which the cf file is generated is an improvement, but its tricky and rigid syntax isn't going to win any awards for friendliness, either. Fortunately, many of the paradigms you might have already been hammered out by others with similar needs and are supplied in the distribution by prepackaged features.

sendmail configuration involves several steps:

+   - Deciding the role of the machine you are configuring: client, server, Internet-facing mail receiver, etc.

+   - Choosing the features needed to implement that role and building an .mc file for the configuration

+   - Compiling the .mc file with m4 to produce a .cf config file

We cover the features commonly used for site-wide, Internet-facing servers and for little desktop clients. For more detailed coverage, we refer you to two pieces of documentation on the care and feeding of sendmail: The O'Reilly sendmail by Bryan Costales et al and the cf/README from the distribution.

# The m4 preprocessor

m4 originally intended as a front end for programming languages, lets users write more readable (or perhaps more cryptic) programs. m4 is powerful enough to use in many input transformation situations, and it works nicely for sendmail configuration files.

m4 macros have the form

```
name(arg1, arg2, ..., argn)
```

There cannot be any space between the name and the opening parenthesis. Left and right single quotes designate strings as arguments. m4's quotes are weird, since the left and right quotes are different characters. Quotes nest, so that m4 has some built-in macros, and users can also define their own. Table 20.8 on the next page lists the most common built-in macros that are used in sendmail configuration.

# The sendmail configuration pieces

The sendmail distribution includes a cf subdirectory which are the pieces necessary for m4 configuration. Table 20.5 on page 776 shows the location of the cf directory if you did not install the sendmail source but relied on your vendor. The README file there is sendmail's configuration documentation.

![](bbox=[0.953, 0.23, 0.983, 0.345])