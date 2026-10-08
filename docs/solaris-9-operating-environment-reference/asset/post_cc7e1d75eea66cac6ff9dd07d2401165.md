
# 424

# genlayoutbl

## Operands

### infile

A path name of an input file. If you specify no input file, genlayoutbl reads from the standard input stream.

## Output and Symbolic Links

If you specify no outfile, genlayoutbl writes output to the standard output. Before you use the system, you must move the generated output file to /usr/lib/locale/local/LO_LTYPE/layout.dat.

The local should also have a symbolic link. /usr/lib/locale/local/LO_LTYPE/locale.layout.so.1, to the 32-bit Universal Multiscript Layout Engine (UMLE), /usr/lib/locale/common/LO_LTYPE/umle.so.1.

For proper 64-bit platform operations, the local should also have a symbolic link, for instance the 64-bit SPARC platform, /usr/lib/locale/common/LO_LTYPE/sparc9/layout.so.1, to the 64-bit UMLE, /usr/lib/locale/common/LO_LTYPE/sparc9/umle.layout.so.1.

The local is that that you want to provide and use the layout functionality you defined.

## Input File Format

A layout definition file of genlayoutbl contains three different sections of definitions.

- Layout attribute definition.
- Bidirectional data and character type data definition.
- Shaping data definition.

For appropriate complex text layout support, all three sections must be defined in the layout definition file.

## Lexical Conventions

The following lexical conventions are used in the layout definition.

| NAME | HEXADIMAL_BYTE | HEXADECIMAL | DECIMAL |
|---|---|---|---|
| | A string of characters that consists of printable ASCII characters. It includes DECIMAL and HEXADECIMAL also. For example, a1_src, b32, 123. | Two-digit hexadecimal number. The number starts with a hexadecimal digit followed by another hexadecimal digit. For example, e0, E1, a7, fe. | A hexadecimal number. The hexadecimal representation consists of an escape character, O followed by the constant x or X, and one or more hexadecimal digits. For example, 0x0, 0x1, 0xA, 0x1b3. | A decimal number, represented by one or more decimal digits. For example, 0, 123, 2165. |

Each comment must start with #. The comment ends at the end of the line.
The following keywords are reserved.

# genlayoutouttbl 425

- active_directional
- active_shape_editing
- ALTI, ALGORITHM_BASIC
- ALGORITHM_IMPLICIT
- AN
- BN
- check_mode
- context
- CONTEXT_LTR
- CONTEXT_RTL
- CS
- EN
- END
- ES
- ET
- FALSE
- FILE_CODE_REPRESENTATION
- implicit_algorithm
- keep
- L
- LAYOUT_ATTRIBUTES
- LAYOUT_BIDI_CHAR_TYPE_DATA
- LAYOUT_SHAPE_DATA
- LRE
- LRO
- MODE_EDIT
- MODE_STREAM
- NSM
- national_numerals
- numerals
- NUMERALS_CONTEXTUAL
- NUMERALS_NATIONAL
- NUMERALS_NOMINAL
- ON
- orientation
- ORIENTATION_CONTEXTUAL
- ORIENTATION_LTR
- ORIENTATION_RTL
- ORIENTATION_TTBLR
- ORIENTATION_TTBR
- PDF

# 426

# genlayoutbi

- PROCESS_CODE_REPRESENTATION
- PS
- R
- repeat
- repeat+
- RLE
- RLO
- S
- shape_charset
- shape_charset_size
- shape_context_size
- swapping
- SWAPPING_NO
- swapping_pairs
- SWAPPING_YES
- TEXT_EXPLICIT
- TEXT_IMPLICIT
- TEXT_NOMINAL
- TEXT_SHAPED
- text_shaping
- TEXT_VISUAL
- TRUE
- type_of_text
- WS.

The following symbols are also reserved as tokens.

( ) [ ] ; ; ... = +

## Layout Attribute Definition

The layout attribute definition section defines the layout attributes and their associated values.
The definition starts with a keyword, LAYOUT_ATTRIBUTES, and ends with END LAYOUT_ATTRIBUTES, as shown in the following example.

```
LAYOUT_ATTRIBUTES

# Layout attributes here.

: END LAYOUT_ATTRIBUTES
```

In the layout attributes section, you can define a total of eight layout attribute value trios, as shown below.

- orientation
- context
- type_of_text
- implicit_algorithm

# genlayoutttbl

- swapping
- numerals
- text_shaping
- shape_context_size

Additionally, you can define five layout attribute value pairs in this section.

- active_directional
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

# 428

# genlayout

The context value trio is meaningful only if the attribute orientation is set to ORIENTATION_CONTEXT. It defines what orientation is assumed when no strong character appears in the text. The possible values are described below.

```
CONTEXT_LTR
```

In absence of characters with strong directionality in the text, orientation is assumed to be left-to-right rows progressing from top to bottom.

```
CONTEXT_RTL
```

In absence of characters with strong directionality in the text, orientation is assumed to be right-to-left rows progressing from top to bottom.

If you specify no value or value trio, the default is CONTEXT_LTR. The type_of_text value trio specifies the ordering of the directional text. The possible values are described below.

```
TEXT_VISUAL
```

Provide code elements in visually ordered segments that can be rendered without any segment inversion.

```
TEXT_IMPLICIT
```

Provide code elements in logically ordered segments. Logically ordered means that the order in which the characters are the same as the order in which the characters would be pronounced when the presented text is read or the order in which characters would be entered from a keyboard.

```
TEXT_EXPLICIT
```

Provide code elements in logically ordered segments with a set of embedded controls.

Some examples of such embedded controls:

- LEFT-TO-RIGHT EMBEDDING (LRE)
- RIGHT-TO-LEFT EMBEDDING (RLE)
- RIGHT-TO-LEFT OVERRIDE (RLO)
- LEFT-TO-RIGHT OVERRIDE (LRO)
- POP DIRECTIONAL FORMAT (PDF)

If you specify no value or value trio, the default is TEXT_IMPLICIT. The implicit_algorithm value trio specifies the type of bidirectional algorithm used in reordering and shaping of directional text. The possible values are described below.

```
ALGORITHM_IMPLICIT
```

Reorder directional elements with an implementation implicit algorithm. The default is ALGORITHM_IMPLICIT.

```
ALGORITHM_BASIC
```

Reorder directional elements with a basic implicit algorithm defined in the Unicode standard.

# 458

Note — Even you can specify two different values for the implicit_algorithm, because the Solaris-defined implicit algorithm is based on the Unicode standard, the behavior is the same whether you choose ALGORITHM_IMPLICIT or ALGORITHM_BASIC for this attribute.

The swapping value trio specifies whether symmetric swapping is applied to the text. The possible values are shown below.

```
SWAPPING_YES
```

The text conforms to symmetric swapping.

```
SWAPPING_NO
```

The text does not conform to symmetric swapping. If no value or value trio, the default is SWAPPING_NO.

The numerals value trio specifies the shaping of numerals. The possible values are shown below. If no value or value trio, the default is NUMERALS_NOMINAL.

```
NUMERALS_NOMINAL
```

National shaping of numerals using the Arabic numbers of the portable character set (in Solaris, ASCII digits).

```
NUMERALS_NATIONAL
```

National shaping of numerals based on the script of the locale. instance, Thai digits in the Thai locale.

```
NUMERALS_CONTEXTUAL
```

Contextual shaping of numerals depending on the context script of surrounding text, such as Hindi numbers in Arabic and Arabic numbers otherwise.

The text_shaping values specify the shaping; that is, choosing (or composing) the correct shape of the input or output text. The possible values are shown below.

```
TEXT_SHAPED
```

The text has presentation form shapes.

```
TEXT_NOMINAL
```

The text is in basic form. If no value or value trio is specified, the default is TEXT_NOMINAL for input and TEXT_SHAPED for output.

The shape_context_size values specify the size of the context (surrounding code elements) that must be accounted for when performing active shaping. If not defined, the default value 0 is used for the number of surrounding code elements at both front and rear.

```
# shape_context_size for both front and rear surrounding code
# elements are all zero.
shape_context_size 0:0
```

The front and rear attribute values are separated by a colon, with the front value to the left of the colon.
