
# Human-Language Modes

A human language is meant eventually to be used by humans, possibly after being formatted by some text-formatting program. Human languages share many conventions about the structure of words, sentences, and paragraphs; with regard to these textual units, the major language modes all behave the same.

Beyond the common region, each mode offers additional functionality oriented to a specific text formatter, such as TeX, LaTeX, or not. Text-formatter extensions are beyond the scope of this presentation; the focus here is on the commands relating to human textual units (for example, words, sentences, and paragraphs).

# Words

As a mnemonic aid, the bindings are defined parallel to the character-oriented controls CONTROL-F, CONTROL-B, CONTROL-D, DELETE, and CONTROL-T. 

Just as CONTROL-F and CONTROL-B move forward and backward over characters, META-A and META-B move forward and backward over words. They may start from a position inside or outside the word to be traversed, but in all cases Point finishes just beyond the word, adjacent to the last character skipped. They accept a numeric argument specifying the number of words to be traversed.

Just as CONTROL-D and DELETE delete characters forward and backward, the keys META-D and META-DELETE kill words forward and backward. They leave Point in exactly the finishing position as META-A and META-B, but they kill the words they pass over. They also accept a numeric argument.

META-I replaces the word before Point with the word after Point.

# Sentences

As a mnemonic aid, three of the bindings are defined parallel to the line-oriented bindings: CONTROL-A, CONTROL-E, and CONTROL-K. As discussed earlier, META-A moves back to the beginning of a sentence, and META-E moves forward to the end. In fact, CONTROL-X deletes back to the beginning of a sentence whereas META-K kills forward to the end of a sentence.

The emacs editor recognizes sentences with a regular expression in a variable named sentence-end. (If you are curious, give the command CONTROL-sentence-end RETURN to view this variable.) Briefly, for the characters `,`, !, followed by two spaces or an end-of-line marker, possibly with close quotation marks or close braces.

The META-A and META-E commands leave Point adjacent to the first or last nonblank character in the sentence. They accept a numeric argument specifying the number of sentences to traverse; a negative argument runs them in reverse.

The META-K and CONTROL-X kill sentences forward and backward, in a manner analogous to CONTROL-K line kill. They leave Point in the same finishing position as META-A and META-E but kill the sentences they pass over. They too accept a numeric argument. CONTROL-X delete is useful for quickly backing out of a half-finished sentence.

# Paragraphs

As discussed earlier, META-i moves back to the most recent paragraph beginning, and META-j moves forward to the next paragraph ending. The META-command marks the paragraph (that is, puts Point at the beginning and Mark at the end) the cursor is currently on, or the next paragraph if it is in between.

The META-l and META-s commands leave Point at the beginning of a line, adjacent to the first character or last character of the paragraph. They accept a numeric argument specifying the number of paragraphs to traverse and run in if given a negative argument.

In human-language modes, paragraphs are separated by blank lines and text-formatter commands, and an indented line starts a paragraph. Recognition is based on the regular expressions stored in the variables paragraph-separate and paragraph-start. A paragraph is composed of complete lines, including the final terminator. If a paragraph starts following one or more blank lines, the last blank line before it belongs to the paragraph.

# Fill

The emacs editor can fill a paragraph to fit a specified width, breaking lines and rearranging them as necessary. Breaking takes place only between words, and there is no hyphen. Filling can be done automatically as you type or in response to your explicit command.

META-X auto-fill-turns Auto Fill Mode on or off. Turn it off by giving the same command. When Auto Fill Mode is on, emacs automatically breaks lines when you type SPACE or RETURN and are currently beyond the specified width line. This feature is useful when you are entering new text.

Auto Fill mode does not refill the entire paragraph you are working on. If you add new text in the middle of a paragraph, Auto Fill breaks your new text as you type but does not refill the complete paragraph. To refill a complete paragraph or Region of paragraphs, use either META-g to refill the current paragraph or META-f-region to refill each paragraph in the Region Point and Mark.

As before, paragraph boundaries are defined by the regular expressions stored in the paragraph-separate and paragraph-start variables.

You can change the filling width from its default value of 70 by setting the filling-column variable with either CONTROL-X to set fill-column to the current cursor position or CONTROL-U nnn to set fill-column to nnn, where 0 is the left margin.

# Case Conversion

The emacs editor can force words or Regions to all uppercase, lowercase, or initial caps (the first letter of each word uppercase, the rest lowercase). Refer to Table 11-15.

## Case Conversion table 11-15

| Command | Description |
| :--- | :--- |
| META-I | Converts word to the right of Point to lowercase |
| META-u | Converts word to the right of Point to uppercase |
| META-c | Converts word to the right of Point to initial caps |
| CONTROL-X-CONTROL-L | Converts Region between Point and Mark to lowercase |
| CONTROL-X-CONTROL-U | Converts Region between Point and Mark to uppercase |

The word-oriented conversions leave Point stationary. The numeric argument converts many words to the right. A negative argument converts many words to the left. Some examples appear in Table 11-15.

# Text Mode

With very few exceptions, the commands for human text units, such as words and sentences, are always turned on, even in programming languages.

# C Mode

In mode TAB runs the function tab-to-stop. Default TAB stops are eight columns. You can adjust them with META+edit-tab-stops, which switches to a special *Tab Stops* buffer, where the current stops are laid out on a scale for you edit. The new stops are installed when you type CONTROL-C, but you are free to kill this buffer (CONTROL-x) or switch from it (CONTROL-x) without changing the stops.

The tab stops you set here affect only the interpretation of TAB characters arriving from the keyboard. The emacs editor automatically inserts enough spaces to reach the stop. This does not affect the interpretation of TAB characters already in the buffer or the underlying file. If you edit the tab stops and use them, you can still print your file, and the hard copy will look the same as the text on the screen.

Programming languages are read by humans but are interpreted by machines. Besides continuing to handle some of the human-language text units, the major language modes address the additional problems of dealing with:

- Balanced expressions enclosed in parentheses, brackets, or braces as textual units
- Comments as textual units
- Indention

In emacs there are Major modes to support C, Fortran, and several variants of Lisp. In addition, many users have contributed modes for their favorite languages. In these modes the commands for human text units are still available, with occasional redefinitions: For example, a paragraph is bounded only by blank lines, and indentation does not signal a paragraph start.

# Expressions

The emacs Major modes are limited to lexical analysis. They can recognize most tokens (for example, symbols, strings, numbers) and all matched sets of parentheses, brackets, and braces. This is enough for Lisp but not for C. The C mode lacks a full-function syntax analyzer and is not prepared to recognize all of C's possible expressions.

> In the emacs documentation the recurring term sex refers to the historic Lisp term S-expression. Unfortunately, it is sometimes used interchangeably with expression, even though the language might not be Lisp at all.
