# 10.1 Overview of the text Widget

A text string can have a tag associated with it. Tags in a text widget are similar to tags in the canvas object. You can apply zero or more tags to a line of text and apply a tag to one or more lines of text. The tags will be discussed in more detail later in this chapter.

A text widget can also have marks associated with it. Marks are similar to tags, except that tags are associated with a text string, a mark is associated with a location in the text. You can have only a single instance of any mark, but you can have multiple marks referring to a single location.

# 10.1.1 Text Location in the text Widget

The text widget does not allow you to place text at any location, the way a canvas widget does. A text widget “fills” from the top left, and you can address any position that has a character defined at that location. If a position outside the range of available lines and characters is requested, it will be mapped to the nearest location in the text widget that has a character defined.

The locations are addressed with index values that are formatted as a list:

+   position ?modifier1 modifier2...modifierN?

The position field may be one of:

+   line.character
The line and character that define a location in the internal representation of the text.

Lines are numbered starting from 1 (to conform to the numbering style of other Unix applications), and character positions are numbered starting from 0 (to conform to the numbering style of C strings).

The character field may be numeric or the word end. The end keyword indicates the position of the newline character that terminates a line.

The x and y parameters are in pixels. This index maps the character with a bounding box that includes this pixel.