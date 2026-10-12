# undefine

This command is the opposite of the **define** command—it takes a variable that has already been defined and undoes the setting. It is useful in situations where a predefined macro that comes with Sendmail has all the settings you want except for one or two that you don't. In these cases, you can undefine the settings you don't want rather than define a new macro by hand.

For example, if you don't expect to ever relay mail over the UNIX to UNIX copy protocol (UUCP), you might want to undefine the variables associated with UUCP transfers.

```
```text
undefine (\`UUCP_RELAY')
```
```

# Using Quotes

As you may have noticed by now, string definition must be in single quotes. These quotes are important to M4 in order to process strings correctly. The beginning quote mark should be the back-tick character (`). This is often found on the same key as the tilde character (~). The end of the quote should be a single quote (') that is often shared with the double quote character ("').

For example:

```
```text
OSTYPE(`linux')
```
```

# The Sendmail Macros

M4 by itself doesn't make configuring Sendmail any easier—it's the macros that ship with the Sendmail package that you can use from within an M4 script that make it easier. In this section, we discuss those macros.

Before reading this section, take a moment to look at the **.me** files that come with Sendmail so that you know what's there. Don't worry if it doesn't make sense yet—seeing what's there and then reading this section will make things work a little more smoothly than the other way around. The main file we'll be concerned with here is /etc/mail/sendmail.mc, but it may also be interesting to browse through all of the .me files in the /usr/share/sendmail-cf/cf/ directory.

# OSTYPE

The **OSTYPE** macro must be used before any of the other macros discussed in this section. It sets up the minimum number of definitions necessary for the particular operating system specified. In our case, we simply need to supply the string **linux** as its parameter, like so:

```
```text
OSTYPE(`linux')
```
```

By using this macro, we spare ourselves from having to configure a number of default settings by hand. You can view the specific features in the /usr/share/sendmail-cf/ostype/linux.mc file that comes with Sendmail.