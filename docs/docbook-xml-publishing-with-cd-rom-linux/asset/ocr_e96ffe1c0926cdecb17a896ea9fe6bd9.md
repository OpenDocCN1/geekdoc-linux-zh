# AuthorInitials

Self-explanatory, the AuthorInitials element holds an author's initials or other brief reference to an author.

The AuthorInitials element uses common attributes.

Example:

```
<author>
  <firstname>Kara</firstname>
  <surname>Pritchard</surname>
  <authorinitials>KP</authorinitials>
</author>
```

# BlockQuote

The BlockQuote element holds a longer quote or citation that is set off from the text.

The BlockQuote element uses common attributes.

Example:

```
<blockquote>
  <attribution>Lloyd Dobler</attribution>
  <para>I don't want to sell anything, buy anything, or process anything as a career. I don't want to sell anything bought or processed, or buy anything sold or processed, or process anything sold, bought, or processed, or repair anything sold, bought, or processed. You know, as a career, I don't want to do that.</para>
</blockquote
```

# Citation

The Citation element makes a reference to a book or publication in the text of the document. The Citation element is used with citations in the body of the document. If you want to cite a work in a bibliography, see the BiblioEntry element.

The Citation element uses common attributes.

Example:

```
<!DOCTYPE para PUBLIC "//OASIS//DTD DocBook V4.1//EN">
<para>
  See <citation>DocBook Publishing</citation> for more help on DocBook.
</para>
```