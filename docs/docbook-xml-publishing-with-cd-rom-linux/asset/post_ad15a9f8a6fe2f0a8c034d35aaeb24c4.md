
# IndexEntry

The IndexEntry indicates an entry in the index that can contain PrimaryIE, SecondaryIE, and other child elements.

The IndexEntry element uses common attributes.

Example:

See Index element example.

# IndexTerm

The IndexTerm element indicates terms that should be indexed. The IndexTerm element is not included in the index markup but is in-line in the regular text.

The IndexTerm uses common attributes.

Example:

```
<para>I use only Linux <idexterm><primary>Operating System</primary><secondary>Open Source</secondary></idexterm> on my computers.</para>
```

# ItemSet

The ItemSet is used in the meta-information of a document to indicate a group of IndexTerms.

The ItemSet element uses common attributes.

Example:

```
<chapter>
<docinfo>
  <itemset>
    <idexterm><primary>DocBook</primary></idexterm>
    <idexterm><primary>SGML</primary></idexterm>
  </itemset>
</docinfo>
</chapter>
```

# Subject

The Subject element indicates a term that describes a document.

The Subject element accepts the following attribute in addition to the common attribute:

- - Weight. Accepts a NUMBER value, has no default, and is not required.

Example:

```
<subjectset>
<subject><subjectterm>DocBook</subjectterm></subject>
<subject><subjectterm>XML</subjectterm></subject>
</subjectset>
```

# SubjectSet

The SubjectSet element contains one or more of the Subject elements.

The SubjectSet element accepts the following attribute in addition to the common attributes:

- - Scheme. Accepts a NAME value, has no default value, and is not required.

Example:

See Subject element example.

# SubjectTerm

The SubjectTerm element holds a term that describes a document. The SubjectTerm is a child element of the Subject element.

The SubjectTerm element uses common attributes.

Example:

See Subject element example.

# Table Elements

The Table elements used in DocBook correspond with the CALS table model.

# Colspec

The Colspec element gives the specifications for a column in a table.

The Colspec element accepts the following attributes:

- - Align. Accepts one of the following values:
  - Center
  - Char
  - Left
  - Justify
  - Right

There is no default value, and the Align attribute is not required.

# Appendix B: DocBook Element Reference

- - Char. Accepts a CDATA value, has no default, and is not required.
- Charoff. Accepts a NUTOKEN value, has no default, and is not required.
- Colnum. Accepts a NUMBER value, has no default, and is not required.
- Colname. Accepts a NMTOKEN value, has no default value, and is not required.
- Colwidth. Accepts a CDATA value, has no default value, and is not required.
- Rowsep. Accepts a NUMBER value, has no default value, and is not required.

Example:

See Table element example.

# Entry

The Entry element holds the information for an entry in a Docbook.

The Entry element accepts the following values:

- - Align. Accepts one of the following values:
  - Center
  - Char
  - Left
  - Justify
  - Right

The Align attribute has no default value and is not required.

- - Char. Accepts a CDATA value, has no default, and is not required.
- Charoff. Accepts a NUTOKEN value and has no default. It is not required.
- Colname. Accepts a NMTOKEN value, has no default, and is not required.
- Colsep. Accepts a NUMBER value, has no default value, and is not required.
- Namest. Accepts a NMTOKEN value, has no default, and is not required.
- Rotate. Accepts a NUMBER value, has no default value, and is not required.
- Rowsep. Accepts a NUMBER value, has no default value, and is not required.

- - Valign. Accepts one of the following values:

  - Bottom
  - Middle
  - Top

The Valign attribute has no default value and is not required.

Example:

See Table element example.

# Entrytbl

The Entrytbl element can be used in place of the Entry element.

The Entrytbl element accepts the following values:

- - Align. Accepts one of the following values:
  - Center
  - Char
  - Left
  - Justify
  - Right

The Align attribute has no default value and is not required.
- Char. Accepts a CDATA value, no default, and is not required.
- Charoff. Accepts a NUTOKEN value, no default, and is not required.
- Colname. Accepts a NMTOKEN value, no default, and is not required.
- Colsep. Accepts a NUMBER value, no default value, and is not required.
- Namest. Accepts a NMTOKEN value, no default, and is not required.
- Rotate. Accepts a NUMBER value, no default value, and is not required.
- Rowsep. Accepts a NUMBER value, no default value, and is not required.

Example:

```
<<tbody>
  <row>
    <entrytbl cols="1" align="left" colnum="1" colname="coll">
      <head>
        <row>
          <ENTRY>FIRST</ENTRY>
          <ENTRY>LAST</ENTRY>
          <ENTRY>M. I. </ENTRY>
        </row>
      </head>
    </row>
</body>
```

# InformalTable

The InformalTable element indicates a table in casual dress. Actually, kidding, it's a table without a title.

The InformalTable element accepts the following attributes:

- - Colsep
- Label
- Frame
- Orient
  - Pgwide
  - Rowsep
- Shortentry
  - ToCenter

Example:

```
<informtable>
<tgroup cols="3">
<colspec align="left" colnum="1">
<<thead>
<row>
  <entry>First Name</entry>
  <entry>Last Name</entry>
  <entry>Middle Initial</entry>
</row>
</thead>
</tgroup>
</informtable>
```

# Row

The Row element indicates a row in a DocBook table.
The Row element accepts the following attributes:

- - Rowsep. Accepts a NUMBER value, has no default value, and is not required.
- Valign. Accepts one of the following values:
  - Bottom
  - Middle
  - Top
The Valign attribute is not required and has no default value.

Example:

See InformalTable element example.

# Spanspec

The Spanspec element provides information for columns in a table that span more than one column. This allows a cell to take up more than one column.
The Spanspec element accepts the following attributes:

- - Align
- Char
- Charoff
- Colsep
- Nameend
- Namest
- Rowsep
- Spanname

Example:

```
<spanspec spanname=header namest=col1 nameend=col2 align="left">
```

# Table

The Table element indicates a DocBook table with a title.

The Table element accepts the following attributes:

- - Colsep
- Label
- Frame
- Orient
- Prowide
- Rowsep
- Shortentry
- ToCentry

Example:

```
<table frame="all"><title>My First Table</title>
<tgroup cols="5" align="left colsep=1 rowspan=1>
<colspec colname=col1>
<colspec colname=col2>
<head>
<row>
  <entry>FIRST</entry>
  <entry>LAST</entry>
  <entry>M.I</entry>
  <entry>D.O.B.</entry>
  <entry>SSN</entry>
</row>
</head>
<tfoot>n<row>
  <entry>n1</entry>
  <entry>n2</entry>
  <entry>n3</entry>
  <entry>d1</entry>
  <entry>s1</entry>
</row>
</tfoot>
<tbody>
<row>
  <entry>Kara</entry>
  <entry>Pritchard</entry>
  <entry>J</entry>
  <entry>8-23-00</entry>
  <entry>123-45-6789</entry>
</row>
</tbody>
</tgroup>
</table
```

# TBody

The TBody element holds rows of a table or an informal table in a DocBook document.

The TBody element accepts the following attribute:

- * Valign. Accepts one of the following values:
  - Bottom
  - Middle
  - Top

The Valign attribute has no default value and is not required.

Example:

See Table element example.

# TFoot

The TFoot element holds any footer information about a table.

The TFoot element accepts the following attribute:

- * Valign. Accepts one of the following values:
  - Bottom
  - Middle
  - Top

The Valign attribute has no default value and is not required.

Example:

See Table element example.

# TGroup

The TGroup element holds the information for all or part of a table.

The TGroup element accepts the following attribute:

- * Align. Accepts one of the following values:
  - Center
  - Char
  - Left
  - Justify
  - Right

The Align attribute has no default value and is not required.

* Char. Accepts a CDATA value, no default, and is not required.

* Charoff. Accepts a NUTOKEN value, no default, and is not required.
