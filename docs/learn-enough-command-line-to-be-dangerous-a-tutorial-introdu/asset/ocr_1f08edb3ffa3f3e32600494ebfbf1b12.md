later modified to *foobar*. Early versions of the Jargon File interpreted this change as a post-war bowdlerization, but it it [sic] now seems more likely that FUBAR was itself a derivative of ‘foo’ perhaps influenced by German *furchtbar* (terrible) — “foobar” may actually have been the *original* form.

Following the link to *metasyntactic variables*, we then find the following:

> **metasyntactic variable**: n.
> 
> A name used in examples and understood to stand for whatever thing is under discussion, or any random member of a class of things under discussion. The word *foo* is the canonical example. To avoid confusion, hackers never (well, hardly ever) use *foo* or other words like it as permanent names for anything. In filenames, a common convention is that any filename beginning with a metasyntactic-variable name is a scratch file that may be deleted at any time.
> 
> Metasyntactic variables are so called because (1) they are variables in the metalanguage used to talk about programs, etc.; (2) they are variables whose values are often variables (as in usages like the value of f(foo,bar) is the sum of foo and bar. However, it has been plausibly suggested that the real reason for the term metasyntactic variable is that it sounds good.

A common pattern when using the command line is changing directories using `cd` (covered in Section 4) and then immediately typing `ls` to view the contents of the directory. This lets you orient yourself and is a good first step toward whatever your next action might be.

One useful ability of `ls` is support for the *wildcard character* `*` (read “star”). For example, to list all files ending in “*txt*”, we would type this: