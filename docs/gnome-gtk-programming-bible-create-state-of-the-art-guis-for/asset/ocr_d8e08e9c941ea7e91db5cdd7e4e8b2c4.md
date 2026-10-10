# GnomeCanvasEllipse

The GnomeCanvasEllipse is a GnomeCanvasItem that draws itself as an ellipse on a GnomeCanvas.

+   - **Inheritance**
+     GnomeCanvasEllipse->GnomeCanvasRE->GnomeCanvasItem->GtkObject
+   - **Function**
+     GkType gnome\_canvas\_ellipse\_get\_type(void)

Chapter 9 provides examples of the GnomeCanvasEllipse widget.

# GnomeCanvasGroup

Objects of this class are created and managed inside a GnomeCanvas widget. Its purpose is to contain and control a collection of CanvasItem objects displayed by the GnomeCanvas. The only way to add a GnomeCanvasItem to a GnomeCanvas is to add it to a GnomeCanvasGroup object. And, because the GnomeCanvasGroup also is a GnomeCanvasItem, it can contain other GnomeCanvasGroups. There is always one GnomeCanvasGroup (the root group) in a GnomeCanvas.

+   - **Inheritance**
+     GnomeCanvasGroup->GnomeCanvasItem->GtkObject
+   - **Functions**
+     - void gnome\_canvas\_group\_child\_bounds(GnomeCanvasGroup \*group, GnomeCanvasItem \*item)
+     - GkType gnome\_canvas\_group\_get\_type(void)

Chapter 9 includes examples of the GnomeCanvasGroup.

# GnomeCanvasImage

A GnomeCanvasImage displays an image on a GnomeCanvas.

+   - **Inheritance**
+     GnomeCanvasImage->GnomeCanvasItem->GtkObject
+   - **Function**
+     GkType gnome\_canvas\_image\_get\_type(void)

You can see examples of using GnomeCanvasImage in Chapter 9.