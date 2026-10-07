
Cary Grant, on the other hand, was versatile enough to play the villain as well as the suave hero in many films.

is formatted by TeX as follows:

```
How do you compare these two terrific leading men? James Stewart had that good-natured, All-American charm mixed with a surprising element of vulnerability, uncommon among other major Hollywood actors. 

Cary Grant, on the other hand, was versatile enough to play the villain as well as the suave hero in many Hitchcock films.
```

You can also insert comments into your TeX file using the $\%$ character. Text following a $\%$ character is treated as a comment and not made part of the TeX output. The text

```
From her% Nothing to do with Hitchcock

% ...nothing at all

e to there
```

is formatted as

```
From here to there
```

TeX has several commands for manipulating paragraphs. The \par command starts a new paragraph, which has the same effect as inserting a blank line.

```
From here \par to there
```

The preceding line is formatted as follows:

```
From here 

to there
```

The \noindent command tells TeX not to indent the paragraph:

```
I grew up on Newcastle Street. 

\noindent That was close to Hazlehurst.
```

This is output as follows:

```
I grew up on Newcastle Street. 

That was close to Hazlehurst.
```

You can also use the escape character before a space in order to force the insertion of an extra space:

```
I think that I need an extra \\ \\ space or two. 

I'm sure of it.
```

This becomes

```
I think that I need an extra space or two.
I'm sure of it.
```

# Fonts

Fonts are representations of characters that share similar size and style. The default font that TeX uses is roman. You can override this by using the internal names that TeX associates with fonts that are externally loaded. You can also add new font definitions. The definitions that TeX knows about by default are: \rm (roman), \tt (typewriter), \bf (bold), \sl (slanted), and \it (italic). TeX continues using whatever font was last specified (including the default) until it is instructed to do otherwise. Therefore, the text

```
This is roman, but I think I will switch to \tt typewriter for a while;
then again, maybe \it italic would be nice. Now back to \rm roman.
```

appears as follows:

```
This is roman, but I think I will switch to typewriter for a while; then again, maybe italic would be nice. Now back to roman.
```

You can add a font and change its size using a command like this:

```
\font \fontname=auxiliary font
```

To use a 12-point roman font, redefine the \rm definition to use the cmr12 auxiliary font, like this:

```
\font\rm=cmr12
We are changing from this font \rm to that font.
```

This formats as follows:

```
We are changing from this font to that font.
```

Fonts have up to 256 different symbols including the standard numeric, uppercase, and lowercase character symbols that you use most frequently. Symbols that are not represented on a standard keyboard can be accessed using the \char command. This command uses the integer that follows it as a character code index into a font's character table. For example, the text

```
TeX would interpret \char 37 as a comment symbol
but it would not
care about a \char 43 sign.
```

is processed by TeX as follows:

```
TeX would interpret % as a comment symbol but it would not care about a + sign.
```

# Controlling Spacing

You've seen how you can insert individual extra spaces in \TeX files. Now, let's examine how you can have more control over the spacing of larger portions of text. \TeX has a series of commands that recognize the following units of measurement:

| Unit | Meaning |
|---|---|
| em | Approximately the width of the character M, depending on the font in use |
| in | Inches |
| pt | Points (1 inch equals 72.27 points) |
| mm | Millimeters (1 inch equals 25.4 millimeters) |

These units are used with decimal numbers to specify the amount of spacing that you need. The \hskip command can insert a horizontal space on a line, like this:

```
\tt From here \hskip 0.5in to there
```

This produces the following output:

From here to there

You can also supply a negative number, which moves the text following the \hskip command to the left (the negative direction). The \hfil command distributes horizontal space in a paragraph when space is available. The interesting thing about the \hfil command is the fact that \TeX inserts one implicitly for each paragraph. Bearing this detail in mind, you can use this command to flush text left or right, or center it on a line, like this:

```
\noindent \hfil Some centered text. \par
```

This is output as follows:

Some centered text.

The \vskip command can insert a vertical space between paragraphs using a given unit of measurement (much like \hskip). The command

```
\vskip 40mm
```

places a vertical space of 40 millimeters between its preceding and succeeding paragraphs. \TeX also provides vertical skipping commands in convenient units: \smallskip, \medskip, and \bigskip.

The vertical equivalent of \hfil is the \vfil command, which can distribute vertical spaces between paragraphs when extra space (non text) is available. \TeX assumes an implicit \vfil command at the end of a document.

You can also explicitly add line breaks and page breaks to your document with the \break command. If this command appears within a paragraph, TeX inserts a line break. If it appears between paragraphs, a page break is inserted. Conversely, you can specify points in your document where you want the text to be kept together and not broken across lines or pages. This is done by using the \nobreak command.

# Page Layout

A page is composed of a header, footer, and body. The header and footer contain information such as chapter title, section heading, and page number. The body is where the main information in your document appears. By changing how this information is ordered in your TeX document, you are actually designing the look of the finished product.

The \headline and \footline commands both take arguments that specify their content. The format of these commands is as follows:

```
\headline=(parameters)
```

The parameters could be a list of things such as a page number command and an \hfil command:

```
\headline={\hfil \the\pageno}
\footline={\hfil}
```

This pair of commands creates a right-justified page number and a blank footer on each page.

You can change the size of the text box that TeX uses for paragraphs by using the \hsize command. For instance, the text

```
\hsize=2in
This text is 2 inches wide but we could choose to make it wider or thinner.
```

produces the following:

```
This text is 2 inches wide but
we could choose to make it
wider or thinner.
```

Margins can be adjusted inward or outward using the \leftskip and \rightskip commands, respectively. By providing positive values to these commands, they move the margin inward, depending on which side you specify (left or right). As you may expect, negative values have the opposite effect: They move the margins outward. Indentation is controlled similarly by using the \parindent command.

The \baselineskip and \parskip commands control the regular vertical spacing between lines and paragraphs, as in the following:

```
\baselineskip=0.15in
\parskip=0.3in
```

*Baseline* refers to the distance between the bottoms of characters (such as $i$) on consecutive lines.

# Using Groups

Normally, TeX continues using such things as fonts and text styles until you explicitly change the format. The grouping features of TeX enable you to define changes that are local to particular sections of text. The formatting originally specified is then restored after the group has been processed.

There are two ways to specify how text is grouped. One is to use the \begingroup and \endgroup command pair. The other is to use the braces { and }. Although both of these perform grouping roles, braces are also used to specify parameters to commands and, as such, must be used with care.

As an illustration of the use of groups in TeX, the text

```
Let's see \begingroup \it how {\bf this grouping stuff} really works \endgroup, shall we?
```

produces the following:

```
Let's see how this grouping stuff really works, shall we?
```

You may have noted from the example that, in fact, groups can contain other groups.

# Mathematical Symbols

One of the most powerful features of TeX is its capability to generate correct mathematical notation for formulas with convenient commands. This is one of the key reasons behind TeX's popularity among engineers and scientists.

TeX distinguishes between formulas that must appear within regular text (inline formulas) and those that must appear on their own line (displayed formulas). You must use the $ symbol to denote inline formulas, as in

```
The equation $2+3=x$ must evaluate to $x=5$.
```

which is generated as the following:

```
The equation 2+3=x must evaluate to x=5.
```
