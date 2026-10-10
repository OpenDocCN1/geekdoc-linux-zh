
![](img/f34d37e3abe9f4517128e54f80ab2616_671_0.png)

Figure 26-4. Xfig is a typical general-purpose vector drawing program.

When you first start xfig, its drawing space is empty. To begin a drawing, click one of the tool buttons along the left side of the window. The top half of this set of buttons provide various shapes—circles, ellipses, curves, polygons, and so on. Buttons for inserting text, bitmap images, and xfig clip art are also present in this area. As a general rule, you place an object by clicking to position one corner, the central point, or a starting point; then moving the mouse and clicking again to position the opposite corner, the outside diameter, or the second point. Some objects, such as polygons, accept an arbitrary number of control points. You click for each one, then click the middle mouse button when you’re done. (For some object types, xfig then draws a final line between the last control point and the first in order to close the figure.)

Most object types provide several drawing options, such as line thickness and style (solid, dashed, and so on), line color, fill color, and fill style. Text objects provide font and font size options. In all cases, you can control these options from buttons that appear along the bottom of the xfig window (Figure 26-4 shows the text object options). One of these options is the object's depth. This characteristic refers to the position of the object in the “stack” of objects in the image. Objects with lower depth numbers obscure those with higher depth numbers when the two are placed over each other.

It’s not uncommon to want to modify objects once you’ve placed them. You can do so by using the editing tools that comprise the bottom panel of the small buttons on the left side of the xfig window. You can use these buttons to group multiple objects into a larger meta-object, break an existing grouping, scale or copy an object, delete an object, edit an object’s characteristics, rotate or mirror an object, and so on. As a general rule, you must click one of the object’s control points (small rectangles placed at an object’s edges or vertices) to modify it, but sometimes clicking anywhere in an object works as well. In most cases, an editing action happens immediately, without further prompting; but sometimes xfig displays a dialog box in which you must enter further information.

![](img/f34d37e3abe9f4517128e54f80ab2616_672_0.png)

> Xfig’s dialog boxes sometimes contain text-entry fields. These operate a bit oddly; to enter text into these fields, your mouse cursor must be over the text-entry field. If you click the mouse in the field and then move it out of the way, you won’t be able to enter text into the text-entry field.

Xfig has a small menu bar from which you can select typical file and editing options. You can save your drawing in xfig’s native format or export it to PostScript, Encapsulated PostScript (EPS), TIFF, and various other formats. From the Edit menu, you can undo operations, cut or paste objects, and so on. The View menu enables you to zoom in and out, display vertex numbers, and so on. The Help menu, of course, provides access to xfig’s help files. Some of these options rely upon external programs, such as a web browser and spell checker. You can adjust the programs upon which xfig relies from the Edit | Global Settings menu.

## Using Dia

Xfig is a useful general-purpose vector graphics package, but sometimes a more specialized tool is in order. Dia (http://www.gnome.org/gnome-office/dia.shtml) is one such tool. Dia is part of the GNOME Office suite described in Chapter 25, and is designed to create diagrams. You can launch it by typing dia in an xterm window. The result is a small control window. To actually use the program, select File | New Diagram; this action creates a drawing window. Figure 26-5 shows both the control window and the drawing window (including a diagram).

Dia provides fewer object types than does xfig, but some of the Dia objects provide options that enable you to accomplish the same goals as xfig objects. For instance, xfig provides separate objects for rectangles with rounded and squared corners, whereas Dia provides a single rectangle tool with an option to change the corner radius, effectively allowing Dia’s single rectangle tool to create both types of rectangle.

![](img/f34d37e3abe9f4517128e54f80ab2616_673_0.png)

Figure 26-5. Dia’s controls are centered around placement of its predefined objects.

Tools near the bottom of the main Dia window enable you to set an object’s color, line thickness and style (solid, dashed, and so on), and end type (plain, arrow, and so on). The color-setting tool works much like the same tool in the GIMP; click the foreground or background rectangle to set a color.

Dia’s strength lies in its range of predefined objects. These objects are collected into various groups, such as Circuit, Flowchart, Logic, and Network. You select an object group by picking it from the selector in the middle of the Dia control window. (This selector is set to Network in Figure 26-5.) When you pick a new object group, the objects available in that group appear below the selector. To place an object, pick it and click in the document window; Dia places the object where you click. You can then right-click the object to obtain a list of actions you can perform on the object, such as viewing the object’s properties (line color, text font, and so on). Some actions are available only when you select several objects; for instance, you can align objects when you select several of them.

To save a Dia file, right-click in the file window and pick File ↓ Save or File ↓ Save As from the resulting context menu. The latter always asks you for a filename, but the former does so only if the file’s not been saved before. You can also export your creation in various other formats, such as EPS and PNG, by picking File ↓ Export.

## Using Gnuplot

The gnuplot (http://www.gnuplot.info) program is a text-based tool for plotting data. This description may sound paradoxical, but it’s not—the program takes a file that contains numerical data and creates a graphics file that displays the data as a graph. This graphics file may optionally be displayed directly in an X window, or you can create a traditional graphics file that you can print, import into a word processor document, or otherwise manipulate.

Contrary to what you might think by the name, gnuplot is not associated with the GNU Project. In fact, gnuplot isn’t covered under the GNU General Public License (GPL), although it is freeware.

To describe gnuplot use, it may be best to begin with an example. Listing 26-1 shows the data file that’s to be plotted. This data file contains raw data in a plain-text format. (Most spreadsheets and other data-analysis tools enable you to export such files, although you may need to manually remove some stray labels.) The first column contains x-axis data points and the second column contains y-axis data points. Listing 26-1 shows the production cost of widgets made by the fictitious Widget Company over time.

```
Listing 26-1. Sample Gnuplot Input Data File

1995 26.34
1996 24.97
1997 25.02
1998 25.67
1999 24.78
2000 23.02
2001 23.69
2002 23.32
```

To create a graph showing these data, follow these steps after installing the gnuplot package or port:

1. Type the data from Listing 26-1 into a text file. In actual use, you would use data from some other source.
2. Create a gnuplot control file. This file contains all the options used to control the creation of a graph from the data file. Listing 26-2 shows such a file, referred to as plot.ctl in the next step. Its options are described shortly.
3. Type **gnuplot -persist plot.ctl**. This command creates an X window in which the data are plotted, as shown in Figure 26-6.

```
Listing 26-2. Sample Gnuplot Control File, plot.ctl

set title 'Widget Cost Over Time'
set xlabel "Year"
set ylabel "Cost"
set output
set terminal x11
plot [1995:2002] [22:28] 'data.txt' with lines
```

If you prefer, you can enter your gnuplot commands (shown in Listing 26-2) interactively. Instead of typing **gnuplot -persist plot.ctl** in Step 3, type **gnuplot**, and then type each of the lines shown in Listing 26-2 at the **gnuplot> prompt**.

Most of the lines in a gnuplot control file set gnuplot options. In Listing 26-2, the first three lines set labels—the graph’s title, the x-axis label, and the y-axis label.

![](img/f34d37e3abe9f4517128e54f80ab2616_675_0.png)
