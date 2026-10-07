# Appendix B: DocBook Element Reference

Example:

```
<para>
For more information, click the <guicon><inlinegraphic>fileref="icons/fmi.gif\></inlinegraphic></guicon> icon below.
</para>
```

# GUILabel

The GUILabel element contains text or a label used in a GUI.

The GUILabel element accepts the following attribute in addition to the common attributes:

+   - MoreInfo. Accepts a value of either None or RefEntry, has the default value None, and is not required.

Example:

```
<para>
The<guilabel>Help</guilabel> screen displays an <guimenu>About</guimenu> menu containing options such as <guimenuitem>Author</guimenuitem><guimenuitem>Application</guimenuitem>, and <guimenuitem>Quit</guimenuitem>.</n</para>
```

# GUIMenu

The GUIMenu element accepts the following attribute in addition to the common attributes:

+   - MoreInfo. Accepts a value of either None or RefEntry, has the default value None, and is not required.

Example:

See GUILabel element example.

# GUIMenuItem

The GUIMenuItem element holds the name of a selection in a GUI.

The GUIMenuItem element accepts the following attribute in addition to the common attributes:

+   - MoreInfo. Accepts a value of either None or RefEntry, has the default value None, and is not required.