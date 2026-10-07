# FieldSynopsis

The FieldSynopsis element is used when providing summary information about a field.

The FieldSynopsis element uses common attributes:

Example:

```
<fieldsynopsis>
  <modifier>...</modifier>
  <type>...</type>
  <varname>...</varname>
</fieldsynopsis>
```

# Filename

The Filename element indicates the name of a file referenced inline.

The Filename element accepts the following attribute in addition to the common attributes:

+   - Class

Example:

```
<filename class="directory">/etc/apt/</filename>
```

# FuncDef

The FuncDef element holds the name of a function in a programming language.

The FuncDef element uses common attributes.

Example:

```
<para>Many programming languages use different syntax to define a function. In pseudocode, defining a function might look like this:</para>
<funcsynopsis>
  <funcprototype>
    <funcdef>function</funcdef> <function>apply()</function></funcdef>
    <paramdef>foo <parameter>par1</parameter></paramdef>
    <paramdef>bar <parameter>par2</parameter></paramdef>
  </funcprototype>
</funcsynopsis>
```

# FuncPrototype

The FuncPrototype element indicates a prototype of a function.

The FuncPrototype element uses common attributes.