
```c
    GNOMEUIINFO_END
});

GnomeUIInfo mainMenu[] = {
    GNOMEUIINFO_SUBTREE("_File",fileMenu),
    GNOMEUIINFO_SUBTREE("_Edit",editMenu),
    GNOMEUIINFO_END
};

int main(int argc,char * argv[])
{
	GtkWidget *app;

    gnome_init("cutpaste","1.0",argc,argv);
    app = gnome_app_new("cutpaste",
		"Cut, Copy, and Paste");
    gtk_signal_connect(GTK_OBJECT(app),"delete_event",
		GTK_SIGNAL_FUNC(eventDelete),NULL);
    gtk_signal_connect(GTK_OBJECT(app),"destroy",
		GTK_SIGNAL_FUNC(eventDestroy),NULL);

    gnome_app_create_menus(GNOME_APP(app),mainMenu);

    text = gtk_text_new(NULL,NULL);
    gtk_widget_set_usize(text,300,200);
    gtk_text_set_editable(GTK_TEXT(text),TRUE);
    gnome_app_set_contents(GNOME_APP(app),text);

    gtk_widget_show_all(app);
    gtk_main();
    exit(0);
}
static void fileExit(GtkObject *object,gpointer data) {
    gtk_main_quit();
}
static void editCut(GtkObject *object,gpointer data) {
    gtk_editable_cut_clipboard(GTK_EDITABLE(text));
}
static void editCopy(GtkObject *object,gpointer data) {
    gtk_editable_copy_clipboard(GTK_EDITABLE(text));
}
static void editPaste(GtkObject *object,gpointer data) {
    gtk_editable_paste_clipboard(GTK_EDITABLE(text));
}
gint eventDelete(GtkWidget *widget,
    GdkEvent *event,gpointer data) {
    return(FALSE);
}
gint eventDestroy(GtkWidget *widget,
    GdkEvent *event,gpointer data) {
    gtk_main_quit();
    return(0);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_489_0.png)

Cut, copy, and paste operations are part of every widget that has `GtkEditable` in its parentage. Most notably, this includes `GtkEntry` (allowing a single line of text to be entered) and `GtkText` (a multiple line, text-editing widget). This example employs a `GtkText` widget. You can use it to cut and paste within a text window, or you can run multiple versions of it and cut and paste among them. You can even cut or copy text from the edit window and paste it into the window of another application that accepts text, such as a text editor or a GNOME terminal.

Line 63 calls `gnome_app_create_menus()` to create the menu bar across the top of the main window. The menus are defined in the arrays on lines 16 through 48 and consist of only two main headings. The File menu has only an Exit entry, and the Edit menu contains Cut, Copy, and Paste. Each of the four menu selections is supplied with its own callback function.

The text widget is created and configured on lines 65 through 68. The call to `gtk_text_new()` on line 65 pass `NULL` for the horizontal and vertical `GtkAdjustment` arguments because this sample does not use scrollbars. The call on line 67 to `gtk_text_set_editable()` specifies that the text is to be accessible from the keyboard and mouse. (A `GtkText` object that is not editable is a display-only text window.)

The callback functions on lines 77 through 85 handle all of the cutting and pasting. The `GtkEdit` widget assumes the responsibility for responding to the mouse, which selects the text to be cut or copied. The widget then highlights the text, extracts the text from the highlighted text, writes the extracted text to the clipboard, reads text from the clipboard, and inserts it into the text window. A call to `gtk_editable_cut_clipboard()` writes the selected text to the clipboard and removes it from the text window. A call to `gtk_editable_copy_clipboard()` does the same, but does not remove the text from the text window. A call to `gtk_editable_paste_clipboard()` reads text from the clipboard and inserts it at the current cursor location.

## Summary

Data can be moved from one application to another under control of the user’s mouse. Graphical objects can be dragged from one location to another, and text can be copied to a global clipboard for insertion into another text window, or into another position in the same text window. The following approaches were explored in this chapter:

- You can use a drag-and-drop operation to transfer any data type of any size, but the sender and the receiver must agree on the data type. This is accomplished using MIME data type names.
- A drag-and-drop operation pre-qualifies a match between the sending and receiving widgets by comparing their respective list of known MIME types.
- A fundamental, drag-and-drop operation is quite simple, but as more data types and more options are added, complexity increases.
- Any editable widget (*GtkText* or *GtkEntry*) can be used to cut and paste text because the complete procedure is included inside the *GtkEditable* class.

The next chapter is about a very special top-level window that is a container of widgets. It is all about the MDI (Multiple Document Interface), which not only acts as a container of child widgets but also allows the user to select among them, and it allows each of the child widgets to modify the menus and toolbars of the parent MDI window.

# Multiple Document Interface (MDI)

**A** *Multiple Document Interface* (*MDI*) is a special window object that has the ability to display one, two, or more child windows. It can show them one at a time (as if they were stacked one on top of the other). It also can add tabs to the side of this stack to allow the mouse to switch from one child window to another. Finally, the MDI window can split itself into multiple, top-level windows and display each of the child windows in its own top-level window.

Because the structure and control of an MDI display differs from normal windows, the MDI object is not a widget. The MDI object acts as a broker between one or more top-level windows and one or more child windows. And, because the number of top-level windows can vary, the MDI object also assumes the responsibility of creating and maintaining the menus and toolbars.

## A Simple MDI Window

The following program is a simple MDI application. It creates and displays four windows and allows the mouse to select which one is visible at any given time. The collection of windows is held in a special container — the MDI object — that allows only one at a time to be visible. In this example, each of the documents is a label widget. The multiple-document window is shown in Figure 17-1.

### In This Chapter

- Creating and displaying a simple MDI window
- Causing an MDI window to display its child windows in different modes
- Changing the options on the menus of an MDI parent window by selecting a child window
- Using a toolbar with an MDI window

![](img/8bcc1ba72831c7d67cfc8b395deab95f_493_0.png)

A display object controlled by the MDI software can have several names. It can be called a document, which fits with the description of it being part of a multiple-document interface. It also is referred to as a view, in that there are different representations of the same, or related, data. Internally, it often is referred to as a child because of its relationship with the MDI container. You also can find references to page because of the way the software flips from one to the other. No matter what you call it, it simply is a widget with its display controlled by the MDI software.

```c
/** simplemdi.c **/
#include <gnome.h>

gint eventDelete(GtkWidget *widget,
	GtkEvent *event,gpointer data);
gint eventDestroy(GtkWidget *widget,
	GtkEvent *event,gpointer data);

static void addChild(GtkObject *mdi,gchar *name);
static GtkWidget *setLabel(GnomeMDIChild *child,
	 GtkWidget *currentLabel,gpointer data);
static GtkWidget *createView(GnomeMDIChild *child,
	 gpointer data);

int main(int argc,char *argv[])
{
	GtkObject *mdi;

	gnome_init("simplemdi", "1.0",argc,argv);
	mdi = gnome_mdi_new("simplemdi", "Simple MDI");
	gdk_signal_connect(mdi,"destroy",
		GTK_SIGNAL_FUNC(eventDestroy),NULL);

	addChild(mdi,"First");
	addChild(mdi,"Second");
	addChild(mdi,"Third");
	addChild(mdi,"Last");

	gnome_mdi_set_mode(GNOME_MDI(mdi),GNOME_MDI_NOTEBOOK);
	gnome_mdi_open_toplevel(GNOME_MDI(mdi));

	gtk_main();
	exit(0);
}
static void addChild(GtkObject *mdi,gchar *name)
{

	GnomeMDIGenericChild *child;

	child = gnome_mdi_generic_child_new(name);
	gnome_mdi_add_child(GNOME_MDI(mdi),
		GNOME_MDI_CHILD(child));
}
```
