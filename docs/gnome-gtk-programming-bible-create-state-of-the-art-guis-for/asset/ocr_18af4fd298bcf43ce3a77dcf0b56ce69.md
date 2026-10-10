**Table 1-3**
**Some Useful Macros**
|XXXX|XXXX|
|----|----|
|ABS(a)|The positive value of a is returned.|
|MAX(a,b)|The numeric value a and b are of the same data type, and the macro returns the larger of the two.|
|MIN(a,b)|The numeric values a and b are of the same data type, and the macro returns the smaller of the two.|
|NULL|This is the address value assigned to a pointer to signify that it points to nothing.|
|TRUE and FALSE|There are many functions that require a gboolean type for an argument. One of these names can be used to pass a constant representing either a true or false condition. Also, if you write a function that returns a gboolean type, it can return one of these names.|

# Utility Functions of glib

This section introduces some of the functions that you will encounter throughout the code—and probably use throughout your application. There are many more functions than the ones I list here, but these are the ones you will encounter in GDK, GTK+, and GNOME source code. Also, you will find a few of them in the example code in this book and, because they can be so handy, you may want to use them yourself.

The functions listed here fall roughly into three categories: memory management, string manipulation, and textual output. There is some overlap among them—for example, a string duplication function may need to allocate memory.

# g_free(gpointer mem)

The previously allocated block of memory at mem is returned to the system.

# g_print(gchar *format,...)

This function is analogous to the standard C function print(). It sends the format string to the standard output after inserting into it the other values passed as arguments.

# g_printerr(gchar *format,...)

This function sends the format string to standard error after inserting into it the other values passed as arguments.