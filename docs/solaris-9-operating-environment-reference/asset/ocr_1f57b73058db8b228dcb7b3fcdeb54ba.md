# 428

# genlayout

The context value trio is meaningful only if the attribute orientation is set to ORIENTATION_CONTEXT. It defines what orientation is assumed when no strong character appears in the text. The possible values are described below.

CONTEXT_LTR

In absence of characters with strong directionality in the text, orientation is assumed to be left-to-right rows progressing from top to bottom.

CONTEXT_RTL

In absence of characters with strong directionality in the text, orientation is assumed to be right-to-left rows progressing from top to bottom.

If you specify no value or value trio, the default is CONTEXT_LTR. The type_of_text value trio specifies the ordering of the directional text. The possible values are described below.

TEXT_VISUAL

Provide code elements in visually ordered segments that can be rendered without any segment inversion.

TEXT_IMPLICIT

Provide code elements in logically ordered segments. Logically ordered means that the order in which the characters are the same as the order in which the characters would be pronounced when the presented text is read or the order in which characters would be entered from a keyboard.

TEXT_EXPLICIT

Provide code elements in logically ordered segments with a set of embedded controls.

Some examples of such embedded controls from ISO/IEC 10646-1 are shown below.

+   - LEFT-TO-RIGHT EMBEDDING (LRE)
- RIGHT-TO-LEFT EMBEDDING (RLE)
- RIGHT-TO-LEFT OVERRIDE (RLO)
- LEFT-TO-RIGHT OVERRIDE (LRO)
- POP DIRECTIONAL FORMAT (PDF)

If you specify no value or value trio, the default is TEXT_IMPLICIT. The implicit_algorithm value trio specifies the type of bidirectional implicit algorithm used in reordering and shaping of directional or context-dependent text. The possible values are described below.

ALGORITHM_IMPLICIT

Reorder directional code elements with an implementation implicit algorithm. The default value is ALGORITHM_IMPLICIT.

ALGORITHM_BASIC

Reorder directional code elements with a basic implicit algorithm defined in the Unicode standard.