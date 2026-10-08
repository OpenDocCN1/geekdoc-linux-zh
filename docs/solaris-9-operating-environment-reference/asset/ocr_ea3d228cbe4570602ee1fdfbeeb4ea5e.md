# genlayoutttbl

+   - swapping
- numerals
- text_shaping
- shape_context_size

Additionally, you can define five layout attribute value pairs in this section.

+   - active_directional
- active_shape_editing
- shape_charset
- shape_charset_size
- check_mode

Each attribute value trio has an attribute name, an attribute value for the input buffer, and an attribute value for the output buffer, as shown in the following example.

```
# Orientation layout attribute trio.
# attribute values are separated by a colon and the left one
# is the input attribute value.
orientation ORIENTATION_LTR:ORIENTATION_LTR
```

Each attribute value pair has an attribute name and an associated attribute value, as shown in the following example.

```
# Shape charset attribute value pair.
shape_charset ISO8859-6
```

The orientation value trio defines the global directional text orientation. The possible values are described below.

```
ORIENTATION_LTR
```

Left-to-right horizontal rows that progress from top to bottom.

```
ORIENTATION_RTL
```

Right-to-left horizontal rows that progress from top to bottom.

```
ORIENTATION_TTBLR
```

Top-to-bottom vertical columns that progress from right to left.

```
ORIENTATION_TTBLR
```

Top-to-bottom vertical columns that progress from left to right.

```
ORIENTATION_CONTEXTUAL
```

The global orientation is set according to the direction of the first significant (strong) character. If the text contains no strong characters and the attribute is set to this value, the global orientation of the text is set according to the value of the attribute context. meaningful only for bidirectional text. If you define no value or value trio, the default is ORIENTATION_LTR.