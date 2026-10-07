
## Element Reference 343

- Colname. Accepts a NMTOKEN value, has no default, and is not required.
- Colsep. Accepts a NUMBER value, no default value, and is not required.
- Rowsep. Accepts a NUMBER value, no default value, and is not required.

Example:

See Table element example.

## THead

The THead element accepts the header information, if any, for a table.

The THead element accepts the following attribute:

- Valign. Accepts one of the following values:
  - Bottom
  - Top

The Valign attribute has no default value and is not required.

Example:

See Table element example.

## Reference Page Elements

The reference page elements in DocBook were originally created for marking UNIX-style manpages. However, the markup for reference pages is very useful for other references as well.

## RefClass

The RefClass element indicates the usability of the reference page.

Example:

See RefEntry element example.

## RefDescriptor

The RefDescriptor element holds the description of a reference page.

Example:

```xml
<refdescriptor>string</refdescriptor>
```

## RefEntry

The RefEntry element indicates an entry in a reference.

Example:

```xml
<refentry id="shutdown">
<refmeta>
<refentrytitle>shutdown</refentrytitle>
<manvolnum>1</manvolnum>
</refmeta>
<refnameddiv>
<refname>shutdown</refname>
<refpurpose>Used to properly shutdown a Linux system</refpurpose>
</refnameddiv>
<refsynopsisdisdiv>
<cmdsynopsis>
<command>/usr/bin/shutdown</command>
</cmdsynopsis>
</refentry>
```

## RefEntryTitle

The RefEntryTitle indicates the title of a RefEntry.

Example:

See RefEntry element example.

## Reference

The Reference element holds a number of the RefEntry elements. A Reference is usually a section, or sometimes even a stand-alone document.

Example:

```xml
<reference><title>My References</title>
<refentry>...</refentry>
...
</reference>
```

## RefMeta

The RefMeta element holds meta-information for a DocBook reference.

Example:

See RefEntry element example.

## RefMiscInfo

The RefMiscInfo element holds meta-information for a reference other than the information contained in the RefMeta element.

Example:

```xml
<refmiscinfo class="pubdate">Published 20011</refmiscinfo>
```

## RefName

The RefName element holds the subject name of a reference.

Example:

See RefEntry element example.

## RefNameDiv

The RefNameDiv element contains the name and classification for a reference page.

Example:

See RefEntry element example.

## RefPurpose

The RefPurpose element holds the description of a reference's purpose.

Example:

See RefEntry element example.

## RefSec1

The RefSec1 element is a level 1 section of a reference.

Example:

```xml
<refsec1 id="rsec1*>
<title>This section</title>
<para>Some more text here</para>
<para>...</para>
</refsec1>
```

## RefSec1Info

The RefSec1Info element contains meta-information about a RefSec1 section.

Example:

```xml
<refsect1info><date>March 21, 2001</date></refsect1info>
```

## RefSection2

The RefSection2 is a level 2 section of a reference.

Example:

See RefSection1 element example.

## RefSection2Info

The RefSection2Info element contains meta-information about a RefSection2 section.

Example:

See RefSection1Info element example.

## RefSection3

The RefSection3 element is a level 3 section of a reference.

Example:

See RefSection1 element example.

## RefSection3Info

The RefSection3Info element holds meta-information about a RefSection3 section.

Example:

See RefSection1Info element example.

## RefSynopsisDiv

The RefSynopsisDiv element holds the synopsis information for a reference.

Example:

See RefEntry element example.

## RefSynopsisDivInfo

The RefSynopsisDivInfo element contains meta-information about a RefSynopsisDiv section.

Example:

See RefEntry element example.

## Obsolete Elements from Previous Versions

Some elements from DocBook version 3.0 are no longer valid DocBook elements. If you need to maintain a document that was written in DocBook 3 or earlier, you must remove these elements and replace them with elements that are used in DocBook 4.

Don't panic, though. Only a few elements from version 3 are obsolete, so it shouldn't be difficult to upgrade to version 4.

## ArtHeader

The ArtHeader element has been replaced in DocBook version 4 with the ArticleInfo element.

## BookBiblio

The BookBiblio element has been removed. There is no replacement.

## Comment

The Comment element has been replaced by the Remark element in DocBook version 4.

## DocInfo

The DocInfo element has been split into a number of more specific elements:
AppendixInfo, BibliographyInfo, ChapterInfo, GlossaryInfo, IndexInfo, PartInfo, PrefaceInfo, RefentryInfo, ReferenceInfo, SetIndexInfo, and SidebarInfo.

## InterfaceDefinition

## SeriesInfo

The SeriesInfo element has been removed.

## Future Versions of DocBook

The DocBook Technical Committee has a road map for XML 5.0. XML is taking off as well, and you can find a wealth of information about XML on the Web to help you get up and running using XML for all sorts of fun and exciting projects.

## Reference Element of DocBook

The DocBook Technical Committee oversees the DocBook updates and revisions, so its site, OASIS, is the best place to check for a new version of DocBook or news about DocBook. The site also posts minutes from the technical committee's meetings, if DocBook is important to your business or organization, you might want to follow what's going on.

The OASIS page also provides a list of tools, commercial and otherwise, that are available for use with DocBook. Finally, if you're looking for a place to ask questions (or answer them), you can sign up for DocBook mailing lists. The mailing lists are low-traffic but occasionally contain good insights into using DocBook.

## Appendix B: Reference Element

The reference page elements in DocBook were originally created for marking UNIX-style manpages. However, the markup for reference pages is very useful for other references as well.

## Appendix C: More DocBook Resources

This explains as thoroughly as possible how to work with DocBook. However, many topics are associated with DocBook—such as SGML, XML, Open Source, and editors—but there just isn't room to cover everything. In this appendix, I provide several resources for you, in case you'd like to strike out on your own and learn more.

## Finding Out More about DocBook

Plenty of information about DocBook is there out on the Web. Many organizations are using DocBook, especially Open Source projects such as the Linux Documentation Project, the GNOME and KDE projects, and many others. If you need to find sample documents and stylesheets, these are great places to store. XML is taking off as well, and you can find a wealth of information about XML on the Web to help you get up and running using XML for all sorts of fun and exciting projects.

The best place to get up-to-date information about DocBook is the OASIS DocBook page (see Figure C.1) at http://oasis.oasis-open/docbook. The DocBook Technical Committee oversees the DocBook updates and revisions, so its site, OASIS, is the best place to check for a new version of DocBook or news about DocBook. The site also posts minutes from the technical committee's meetings, if DocBook is important to your business or organization, you might want to follow what's going on.

The OASIS page also provides a list of tools, commercial and otherwise, that are available for use with DocBook. Finally, if you're looking for a place to ask questions (or answer them), you can sign up for DocBook mailing lists. The mailing lists are low-traffic but occasionally contain good insights into using DocBook.

## Open Source Publishing

The official documentation for DocBook is DocBook: The Definitive Guide, published by O'Reilly and Associates. DocBook: The Definitive Guide is also
