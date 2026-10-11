With `format_name()` in place, the implementation of the `text_format_entry()` function that prints an entry becomes almost completely trivial:

```
```
sub text_format_entry
{
	print "$_\n", format_name ($_\[0\]);
}
```
```

# 8.3.1.2  Generating the Rich Text Format Directory

Generating the RTF version of the directory is a little more involved than generating the member list for the annual meeting program. For one thing, we need to print more information from each entry. For another, we need to put out some RTF control language with each entry to achieve the effects that we want, and some control language at the beginning and end of the document. A minimal RTF document framework looks like this:

```
```c
{
\rtf0
\fonttbl {\f0 Times;}
\plain \f0 \fs24
...document content goes here...
}
```
```

The document begins and ends with curly braces `{` and `}`). RTF keywords begin with a backslash, and the first keyword of the document must be `\rtfn`, where `n` is the version number of the RTF specification that the document uses. Version 0 is fine for our purposes.

Within the document, we specify a font table to indicate the font to use for the entries. Font table information is listed in a group consisting of curly braces containing a leading `\fonttbl` keyword and some font information. The font table in the framework just shown defines font number 0 to be in Times. (We need only one font, but you could use more if you wanted to be fancier.)

The next few directives set up the default formatting style: `\plain` selects plain format, `\f0` selects font 0 (which is defined as Times in the font table), and `\fs24` sets the font size to 12 points (the number following `\fs` indicates the size in half-points). It’s unnecessary to set up margins because most word processors will supply reasonable defaults.

The initialization and cleanup functions produce the document framework. They look like this (note the doubled backslashes to get single backslashes in the output):

```
```
sub rtf_init
{
	print "{\\rtf0\n";
	print "\\fonttbl {\\f0 Times;}\n";
	print "\\plain \\f0 \\fs24\n";
}
```

```
sub rtf_cleanup
{
```
```