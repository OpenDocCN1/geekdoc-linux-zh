# 1442

# troff

-tdest Prepare output for typesetter dest. The following values can be supplied for dest.

+   * post A PostScript printer (the default). You must pipe the output through dpost(1) before it is sent to the PostScript printer to get the proper output.
* aps Autoglic APS-5.
* -uN Set the bold factor for the font mounted in 3 to M If missing, then set the bold factor to 0.
* -z Suppress formatted output. Output only diagnostic messages and messages output using the .tm request.

# Operands

filename The file containing text to be processed by troff.

# Examples

The following example shows how to print an input text file,mytext, coded with formatting requests and macros. The input file contains equations and tables and must go through the tbl(1) and eqn(1) preprocessors before it is formatted by troff with ms macros, processed by dpost(1) and printed by lp(1).

```
castle mytext | eqn | troff -ms | dpost | lp
```

# Files

+   * tmp/trtmp Temporary file.
* /usr/share/lib/tmac/* Standard macro files.
* /usr/lib/font/* Font-width tables for alternative mounted troff files.
* /usr/share/lib/nterm/* Terminal-driving tables for nroff.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNdoc |

# See Also

checknr(1), col(1), dpost(1), eqn(1), lp(1), man(1), nroff(1), tbl(1), attributes(5), man(5), me(5), ms(5)