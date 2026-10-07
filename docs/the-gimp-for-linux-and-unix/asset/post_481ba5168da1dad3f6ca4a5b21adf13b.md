
# Chapter 14

16. Type xfstst --sync at the command prompt, then press Enter on the keyboard (Figure 24).

17. Type xfstst & at the command prompt, then press Enter on the keyboard.

18. Type xset fp+ unix/:7101 at the command prompt, then press Enter on the keyboard.

19. Type exit at the command prompt, then press Enter on the keyboard. This will log you out as root and return to your regular log in. Congratulations! You made it! Launch the GIMP and use the Text Tool to use your new True fonts (Figure 25).

```
Terminal
File Edit Settings Help
Found 23 fonts.
[root@localhost xfstst-1.0]$ mkdir /usr/share/fonts/trustype
[root@localhost xfstst-1.0]$ xfstst --sync
Found 23 fonts.
[root@localhost xfstst-1.0]$ cp xfstst /usr/share/fonts/trustype/
[root@localhost xfstst-1.0]$ xset fp+ unix/:7101
```

Figure 24. Type xfstst --sync and press Enter on the keyboard. This makes the xfstst program locate the True fonts.

## Tips

- If you want to add new TrueType fonts to your computer, copy them into the /usr/share/fonts/trustype directory, open a terminal window and type xfstst --sync at the command prompt, then press Enter on the keyboard.

- There is a way to set the xfstst program to run automatically when you boot your computer (which makes the TrueType fonts available), but it's dicey. I'm not including it because I tried it and it totally crashed my computer (ugh!). I spent the better part of a morning getting my computer up and running again.

- If you add new fonts to the TrueType font directory, they know they're there. Just open a terminal window and type xfstst --sync at the command prompt, then press Enter on the keyboard.

![](img/5164bc49fb24f10213e18cc994b7b40c_239_0.png)

Figure 25. After restarting the GIMP, use the Text Tool to view your new fonts.

```
Downloading TrueType Fonts
There are thousands of free TrueType fonts ready for download from the Web. Check out Type Euphoria at:
http://fonts.linuxpower.org/
```

216

## Transforming Text

Rotating, scaling, shearing, adding perspective, flipping, and moving text is easy whether it's on its own layer or part of a layer containing an image.

To rotate, scale, shear, or add perspective to text:

- 1. Use one of the selection tools to select the text you want to rotate (Figure 27) or use the Layers & Channels dialog box to select a text for rotation.
2. Double-click on the Transform Tool in the GIMP Toolbox. The Tool Options dialog box will open (Figure 27).
3. In the Transform area, select the region button next to one of the options—Rotation, Scaling, Shearing, or Perspective.
4. Select the Smoothing check box if you want the edges of the text blurred to create a smoother look.
5. Click Close. The Tool Options dialog box will close.
6. With the Transform Tool selected, position the mouse pointer over the text or layer.
7. Press the left mouse button and drag. The selected text or layer will rotate, scale, shear, or add perspective, depending upon the option you selected (Figure 28).

![](img/5164bc49fb24f10213e18cc994b7b40c_240_0.png)

Figure 26. Use a selection tool to select the text you want to transform.

![](img/5164bc49fb24f10213e18cc994b7b40c_240_1.png)

Figure 27. Use the Tool Options dialog box to select the type of transformation.

![](img/5164bc49fb24f10213e18cc994b7b40c_240_2.png)

Figure 28. Drag the mouse to transform the text. In this example, perspective has been added to the text.

## Tip

- To find out more about the Transform Tool and what it can do, turn to pages 154–162.

![](img/5164bc49fb24f10213e18cc994b7b40c_240_3.png)

## To flip text vertically or horizontally:

- Use one of the selection tools to select the text you want to flip (Figure 29). Use the Layers & Channels dialog box to select a text layer for flipping.

- Double-click on the Flip Tool in the GIMP Toolbox. The Tool Options dialog box will open (Figure 30).

- Select either the Horizontal or Vertical radio button.

- Click Close. The Tool Options dialog box will close.

- With the Flip Tool selected, click on the selected text or layer. The selection or layer will flip horizontally or vertically, depending on the option you selected (Figure 31). You can create interesting results using several transformations (Figure 32).

![](img/5164bc49fb24f10213e18cc994b7b40c_241_0.png)

![](img/5164bc49fb24f10213e18cc994b7b40c_241_1.png)

- Tip: To find out about the Flip Tool, turn to pages 152–153.

![](img/5164bc49fb24f10213e18cc994b7b40c_241_2.png)

![](img/5164bc49fb24f10213e18cc994b7b40c_241_3.png)

## Working with Text

**Figure 33.** Use the Text Tool to create text.

## To move a text layer:

- 1. Use the Text Tool to create some text (**Figure 33**). It will appear (**Figure 33**).
2. In the Layers & Channels dialog box, anchor the text.
3. Select the Move Tool from the GIMP Toolbox.
4. Position the mouse pointer over the text, press the left mouse button and drag. (**Figure 34**).

- Tip: To find out how to move text, turn to page 148.

## It's Easy to Add Outline to Text

- 1. Use the Text Tool to create text. It will appear as a floating selection.
- 2. Use the Brush tool to select the text you want to outline.
- 3. Set the foreground color to the color you want.
- 4. Right-click on the image and choose Dialogs→Stroke.

## Filling Text with a Pattern

To fill text with a pattern:

- 1. Use the Text Tool to create the text you want to fill (Figure 35). It will appear as a floating selection.
2. Double-click the Bucket Fill Tool in the GIMP. The Tool Options dialog box will open (Figure 36).
3. In the Fill area, select the Pattern radio button.
4. Click Close. The Tool Options dialog box will close.
5. Right-click on the image and choose Dialogs→Patterns (Figure 37).
6. Select a pattern in the Pattern Selection dialog box.
7. With the Bucket Fill Tool selected, position the mouse cursor over one of the letters and click. The pattern will fill the letter (Figure 39).
8. Continue filling the other letters with the same or a different pattern (Figure 40).

![](img/5164bc49fb24f10213e18cc994b7b40c_243_0.png)

Figure 35. Create the text you want to fill.

![](img/5164bc49fb24f10213e18cc994b7b40c_243_1.png)

Figure 36. In the Tool Options dialog box, select the Pattern radio button.

| Fill | |
|---|---|
| Gradient Editor | Ctl+G |
| Layers & Channels...... | Ctl+L |
| Tool Options... | |

| File | |
| Edit | |
| Select | |
| View | |
| Image | |
| Layers | |
| Tools | Brushes... Shft+B |
| Script-Fu | Patterns... Shft+P |
| Dialogs | |
| Palette... | Ctl+P |

Figure 37. Right-click on the image and choose Dialogs→Patterns.

Figure 38. Use the Pattern Selection dialog box to select a pattern.

Figure 39. When you click, the pattern fills the letter.

Figure 40. Continue filling the rest of the letters with the same or a different pattern.

220

![](img/5164bc49fb24f10213e18cc994b7b40c_244_0.png)

![](img/5164bc49fb24f10213e18cc994b7b40c_244_1.png)

![](img/5164bc49fb24f10213e18cc994b7b40c_244_2.png)
