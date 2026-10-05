
Paint operations are, however, restricted to a rectangular area that encloses the floating selection. If you want to enlarge the floating selection beyond this, you must first enter the corresponding layer. To do this, you click on the floating selection layer in the LAYERS dialog and execute RESIZE LAYER.

- In floating selections, the BUCKET FILL command functions differently than in normal selections (in the way described on page 67). If you want to fill the entire contents of a floating selection with the background color, you need to use the EDIT | FILL command instead of BUCKET FILL.
- The degree of transparency of the floating selection can be freely set in the LAYERS dialog (OPACITY ruler). This can be used to make a selection transparent.
- You can convert a floating selection into a normal layer. All you need to do is double click in the LAYERS dialog and give it a new name.

## Normal selections versus floating selections

Many GIMP operations function the same way as floating selections and normal selections, in that their effect is limited to the selected area.
Though floating selections look like selections, they are not selections. This is why the SELECT commands do not work, and this is why it is also not possible to invert a floating selection by simply pressing Ctrl+I.

> In addition to an existing floating selection, a normal selection can be made inside or outside. The floating selection is then only visible in the area of this selection. however, the location of the normal selection remains unchanged when the floating selection is moved. This can make simultaneous working with a floating selection and a normal selection quite confusing. Occasionally, however, this combination is a useful aid for restricting the scope of a movable selection.

## Dissolving floating selections

Unless you have activated a paint tool in the toolbox, a simple mouse click on the floating selection is sufficient to integrate the floating selection back into the image. The same effect can also be achieved with the LAYERS | ANCH command or with Ctrl+H. Reversion of a floating selection into a normal selection is unfortunately not possible.

## Copying and pasting of selections

In nearly all programs, a selected area can be copied into a buffer with Ctrl+C or cut with Ctrl+X, Ctrl+V pastes the selection into the image — evidently as a floating selection.

## BEZIER CURVES

In addition, the EDIT menu provides some more exotic commands: PASTE INTO is a variation of PASTE where, prior to the pasting operation itself, a new selection must be created. With PASTE INTO, the content of the clipboard is inserted and cut off by the boundary of the selection. As with the normal PASTE, the floating selection can still be moved after the command.

NAMED COPY or CUT can be used to copy the copied or cut selection name which can be later used to paste the selection. The advantage is that you can store several floating selections on the clipboard and access them when needed. If you use the XCF format, this clipboard is saved in the file!

## Moving and transforming selections

The Gimp User Manual states that 'moving selections in Gimp is not altogether intuitive' — and you will probably agree. After you have selected an area, you can easily move it with the mouse. If you want to move the area a second time, it is immediately glued to the image (More precisely: the floating selection was amalgamated with the image).

The reason for this strange behavior: selections can be moved without problems, but they are automatically converted into floating selections. (The same applies to all operations discussed in this). In floating selections, a normal mouse click has a different meaning from the one it has in simple selections – it corresponds to the LAYERS ANCH command. Obviously, you can also move floating selections — but by doing so, you must first activate the MOVE tool of the toolbox!

MOVE is only designed for use with layers (including the special case of floating selections), but not with normal selections. If you have carried out a normal selection and employ MOVE, you move not only the selection, but the entire layer.

> CAUTION
While MOVE is active, the floating selection can also be moved by means of the cursor keys. However, each keyboard input is counted as a separate operation, so that the few undo are quickly exhausted.

Selections and floating selections can be mirrored, rotated, distorted, and otherwise transformed by means of the two commands TRANSFORM and FLIP. Handling these tools is simple – just open the corresponding dialog with a double click on the toolbox.

> TIP
When using perspective with TRANSFORM, you should avoid excessive enlargement – otherwise the image will become visibly blurred. Also avoid carrying out too many transformations in sequence – with each of these, the image loses quality (definition).

## 690 GIMP - THE PHOTOSHOP ALTERNATIVE

![](img/b30873dd3d753687a59253fb9ad26a0b_717_0.png)

Figure 20.19 Application sample of Flip, Rotation, and perspective distortion.

## Creating a frame around a selection edge (Stroke)

With EDIT | STROKE, you can follow the edge of a selection with a pencil. Prior to carrying out this command, select an appropriate pencil (BRUSHES dialog), and experiment with the SPACING setting of this dialog. To paint the image shown in Figure 20.20, a circle was selected, and the ‘Diagonal Star’ pencil was applied with a SPACING of 100.

![](img/b30873dd3d753687a59253fb9ad26a0b_717_1.png)

Figure 20.20 An aureole created with Gimp.

> TIP When you work with a floating selection, you should deactivate the KEEP TRANSPARENCY option in the LAYERS dialog to make the floating selection transparent.

## Layers, masks, and channels

When you work with a floating selection, you should deactivate the KEEP TRANSPARENCY option in the LAYERS dialog to make the floating selection transparent. however, the location of the normal selection remains unchanged when the floating selection is moved. This can make simultaneous working with a floating selection and a normal selection quite confusing. Occasionally, however, this combination is a useful aid for restricting the scope of a movable selection.

