# Editor

The Editor element holds information about the editor of a DocBook document or cited work.

The Editor element uses common attributes.

Examples:

See Contrib element sample.

# Epigraph

The Epigraph element holds an epigraph for a chapter, a section, or another DocBook element.

The Epigraph element uses common attributes.

Example:

```
<!DOCTYPE chapter PUBLIC "//OASIS//DTD DocBook V4.1//EN">
<chapter>
  <title>...</title>
  <epigraph>
    <attribution>Einstein</attribution>
    <para>Mathematics deals exclusively with the relations of concepts to each other without consideration of their relation to experience.</para>
  </epigraph>
</chapter>
```

# FirstName

The FirstName element holds the first name of an author, an editor, or other meta-information element. The FirstName element isn't used to designate every first name mentioned in the text of a document.

The FirstName element uses common attributes.

Example:

```
<firstname>Joe</firstname>
```

# Footnote

The Footnote element creates a footnote. The Footnote element is very convenient for authors because it requires no special formatting or worries about placement of the footnote in layout. Simply use the Footnote element in-line text you want to footnote, and the processing system will handle setting it off from the text.