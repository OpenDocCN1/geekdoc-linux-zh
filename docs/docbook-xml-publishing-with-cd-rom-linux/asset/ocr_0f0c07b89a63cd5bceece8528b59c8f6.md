# Chapter 2: Writing a Technical Article

attribute. The class attribute has three possible values: Directory, HeaderFile and SymLink.

```
<para>
Now open the file <filename>passwd</filename> in the <filename
class="directory">*/etc/</filename> directory.
</para>
```

The filename element enables you to further specify certain classes of names: Directory, HeaderFile, or SymLink.

# The ItemizedList Element

The ItemizedList element contains a number of items designated by the ListItem element. The ItemizedList element generates a list of bulleted items instead of numbered items. See the ListItem element next for an example of its use.

# The ListItem Element

The ListItem element is used in the ItemizedList and OrderedList elements. Unlike the <li> tag in HTML, the ListItem element requires that a element be nested inside it. Generally, the ListItem output is part of a bulleted or numbered list. In the following example, you also see that the ListItem element is not an empty element, unlike the <li> HTML tag.

```
<para>The world's best bands are</para>
<itemizedlist>
<list>
<para>The Beatles</para>
</list>
<list>
<para>The Who</para>
</list>
<list>
<para>Pink Floyd</para>
</list>
</itemizedlist>
<para>Note that Britney Spears is not on the list.</para>
```

Figure 2.5 shows what the markup looks like in the Vim editor, with syntax highlighting. More on Vim and using syntax highlighting can be found in Chapter 9.