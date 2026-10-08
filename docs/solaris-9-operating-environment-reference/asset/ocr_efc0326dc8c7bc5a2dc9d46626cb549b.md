# genlayouttbl 435

contextual_range : HEXADECIMAL
HEXADECIMAL '...' HEXADECIMAL

For example,

# National numerals definition. The national number that
# replaces Arabic number 0 to 9 is 0, 0x41, 0x42, and so on.
# The contextual surrounding characters are 0x20 to 0x40 and
# 0x50 to 0x7f.

national_numerals.
(0x0, 0x41, 0x42, 0x43, 0x44, 0x45, 0x46, 0x47, 0x48, 0x49)
; 0x20...0x40, 0x50...0x7f

Unless NUMERALS_CONTEXTUAL is the value of the numerals attribute, the contextual
range definition is meaningless.

# Shaping Data Definition

The shaping data definition defines the context-dependent shaping rules that
are used in the shaping algorithm of the UMLE.
The definition starts with a keyword, LAYOUT_SHAPE_DATA, and ends with END
LAYOUT_SHAPE_DATA, as shown in the following example.

LAYOUT_SHAPE_DATA
# Layout shaping data definitions here.

The shaping data definition should be defined for the two different kinds of text shape
forms, TEXT_SHAPED and TEXT_NOMINAL, depending on the text-shaping attribute value
and for the two different kinds of text representations, file-code representation and
process-code representation (that is, wide-character representation).

LAYOUT_SHAPE_DATA
FILE_CODE_REPRESENTATION
_SHAPED

```
# TEXT_SHAPED shaping data definition in file code
# representation here.
```

END TEXT_SHAPED

TEXT_NOMINAL

```
# TEXT_NOMINAL shaping data definition in file code
# representation here.
```

END TEXT_NOMINAL