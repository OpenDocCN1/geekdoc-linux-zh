Similarly, you can change the selection by using "**tag add**" to set a new selection, or "**tag remove**" to remove the selection. You can't actually delete the "self" tag of course.

> *Though the default widget bindings prevent this from happening, "self" is like any other tag in that it can support multiple ranges, i.e. disjoint selections. To prevent this from happening when changing the selection from your code, make sure you remove any old selection before adding a new one.*

The text widget manages the concept of the insertion cursor (where newly typed text will appear) separate from the selection. It does so using a new concept called a mark.

# Marks

Marks are used to indicate a particular place in the text. In that respect they are like indices, except that as the text is modified, the mark will adjust to be in the same relative location. In that way they are resemble tags, but refer to a single position rather than a range of text. Marks actually don't refer to a position occupied by a character in the text, but specify a position between two characters.

Tk automatically maintains two different marks. The first is named "insert", and is the present location of the insertion cursor. As the cursor is moved (via mouse or keyboard), the mark moves with it. The second mark is named "current", and reflects the position of the character underneath the current mouse position.

To create your own marks, use the widget's "**mark set**" method, passing it the name of the mark, and an index (the mark is positioned just before the character at the given index). This is also used to move an existing mark to a different position. Marks can be removed using the "**mark unset**" method, passing it the name of the mark. If you delete a range of text containing a mark, that also removes the mark.

The name of a mark can also be used as an index (in the same way "1.0" or "end-1c" are indices). You can find the next mark (or previous one) from a given index in the text using the "**mark next**" or "**mark previous**"methods. The "**mark names**" method will return a list of the names of all marks.

Marks also have a gravity, which can be modified with the "**mark gravity**" method, which affects what happens when text is inserted at the mark. Suppose we have the text "ac", with a mark in between that we'll symbolize with a pipe, i.e. "a|c". If the gravity of that mark is "right" (the default) the mark will attach itself to the "c". If the new text "b" is inserted at the mark, the mark will remain stuck to the "c", and so the new text will be inserted before the mark, i.e. "ab|c". If the gravity is instead "left", the mark will attach itself to the "a", and so new text will be inserted after the mark, i.e. "a|bc".

# Images and Widgets

Like canvas widgets, text widgets can contain not only text, but also images and any other Tk widgets (including a frame itself containing many other widgets). In some senses, this allows the text widget to work as a geometry manager in its own right. The ability to add images and widgets within the text opens up a world of possibilities for your program.

Images are added to a text widget at a particular index, with the image normally specified as an existing Tk image. There are also other options that allow you to fine-tune padding and so on.