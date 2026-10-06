# Cut-and-Paste Mouse Commands (Continued)

Double-Drag-Mouse-1
("dit-dahhh")
Selects and highlights a contiguous region of syntax units for this
mode.

Triple-Mouse-1
Selects and highlights the region around the clicked-on line.
Mouse-3 region adjustments will be made in line granules.

Triple-Drag-Mouse-1
("dit-dahhh")
Selects and highlights a contiguous region of complete lines.

Table 11-25 shows the suggested mouse-oriented methods (by no means
only methods) to accomplish some common editing actions.

# Edit with a Mouse

Killing text
Click Mouse-1 at one end, Double-Mouse-3 at the other. To see the
domed region clearly, give just one Mouse-3, and the area will be
highted. Then you can give a second Mouse-3 (don't move the
mouse between clicks), and the highlighted area will disappear.
killed text can be pasted elsewhere in emacs with CONTROL-Y or
Mouse-2 or possibly in another X application (often, not always,
using Mouse-2 at that end)

Marking a region
Use Drag-Mouse-1 if the desired region is onscreen; otherwise, use
Mouse-1 and Mouse-3. The highlighted region is the Kill Ring,
just as you have put there with META--, and it can be copied
elwhere in emacs with CONTROL-Y or Mouse-2 into another X
application. This region is delimited by Point and Mark is
therefore accessible to all the region-oriented commands.

Importing text
Cut the text in another X application, and switch to an emacs frame
window. CONTROL-Y or Mouse-2 will insert the cut text at Point.

# Mouse-2 Selections

Yanking text is not common or even meaningful in every buffer (for example, dried,
info, compilation), and for these buffers highlighting and Mouse-2 are often man-
age differently in a mode-sensitive manner. The usual scheme is to highlight some
of the buffer objects by positioning the mouse over them and then to operate on
sobject by clicking Mouse-2. The “operation” is package-specific; for dried, the file