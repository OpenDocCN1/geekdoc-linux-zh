RenderAs. Accepts one of the following values:

+   - Sect2
- Sect3
- Sect4
- Sect5

The Renderas attribute is used by the processing system, has no default value, and is not required.

Status. Accepts a CDATA value, has no default value, and is not required.

Example:

```
<!DOCTYPE chapter PUBLIC "//OASIS/DTD DocBook V4.1//EN">
<chapter>
  <title>Chapter 1</title>
  <para>...</para>
  <sect><title>Introduction</title>
  <para>...</para>
  </sect>
</chapter>
```

# Sect2

The Sect2 element begins a level 2 section in a document. The Sect2 element may contain a Sect3 element directly but not a Sect4 element—you cannot skip Sect elements.

The Sect2 element accepts the following attributes in addition to the common attributes:

+   - Label. Accepts a CDATA value, has no default value, and is not required.
- RenderAs. Accepts one of the following values:
- Sect1
- Sect3
- Sect4
- Sect5

The RenderAs attribute is used by the processing system, has no default value, and is not required.

Status. Accepts a CDATA value, has no default value, and is not required.

Example:

```
<!DOCTYPE sect1 PUBLIC "//OASIS/DTD DocBook V4.1//EN">
<sect><title>Introduction</title>
<para>...</para>
```