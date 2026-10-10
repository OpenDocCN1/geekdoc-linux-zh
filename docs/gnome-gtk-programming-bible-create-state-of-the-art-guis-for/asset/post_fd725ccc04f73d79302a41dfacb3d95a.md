
# Chapter 19: Configuration and Internationalization

## Configuration Retrieval

```c
void gnome_config_get_vector(const char *path,
int *argcp, char ***argvp)
void gnome_config_get_vector_with_default(
const char *path, int *argcp, char ***argvp,
gboolean *def)
void gnome_config_private_get_vector(const char *path,
int *argcp, char ***argvp)
void gnome_config_private_get_vector_with_default(
const char *path, int *argcp, char ***argvp,
gboolean *def)
```

If the value is not found in the configuration file, an empty array is returned. If the `def` argument is specified, the `gboolean` value it points to is set to `TRUE`—if the value is found in the file. It is set to `FALSE` if the default value is returned.

## Internationalization

If it is possible that your application may wind up being translated into another language (and with the Internet being what it is today, it’s quite likely), there are some steps you can take to facilitate translation. If, inside your source code, you correctly mark the strings that should be translated, the translation process can be automated. While a human translator is necessary to translate each of your text strings into the other language, your application checks its environment to determine which language to use.

The process is quite simple. The following example shows how to do the initial setup, and how to declare strings so they are available for translation.

```c
/* translate.c */
#include <gnome.h>

#define PACKAGE "translate"
#define GNOMELOCALEDIR "/usr/share/locale"

GtkWidget *makeBox();
gint eventDelete(GtkWidget *widget,
GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget,
GdkEvent *event, gpointer data);

static gchar *labelstring = N_("Static string");

int main(int argc, char *argv[])
{
    bindtextdomain(PACKAGE, GNOMELOCALEDIR);
    textdomain(PACKAGE);

    gnome_init("translate","1.0",argc,argv);
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_container_set_border_width(GTK_CONTAINER(window),
                25);
    gtk_signal_connect(GTK_OBJECT(window),"delete_event",
                GTK_SIGNAL_FUNC(eventDelete), NULL);
    gtk_signal_connect(GTK_OBJECT(window),"destroy",
                GTK_SIGNAL_FUNC(eventDestroy),NULL);

    box = makeBox();
    gtk_container_add(GTK_CONTAINER(window),box);
    gtk_widget_show(window);
    gtk_main();
    exit(0);
}
GtkWidget *makeBox() {
    GtkWidget *box;
    GtkWidget *button;

    box = gtk_vbox_new(FALSE,0);
    gtk_widget_show(box);

    button = gtk_button_new_with_label(_("Inline string"));
    gtk_box_pack_start(GTK_BOX(box),button,FALSE,FALSE,0);
    gtk_widget_show(button);

    button = gtk_button_new_with_label(_(labelstring));
    gtk_box_pack_start(GTK_BOX(box),button,FALSE,FALSE,0);
    gtk_widget_show(button);

    return(box);
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

The definition of `PACKAGE` on line 4 assigns a package name to the program. There can be more than one application in a package. Any strings that are shared among applications only need to be translated once because they both use the same lookup tables. The definition of `GNOMELOCALEDIR` on line 5 specifies the directory that will hold the translation files. This directory is where the software will look when it needs to make a translation.

### Note

The definitions of `PACKAGE` and `GNOMELOCALEDIR` normally are defined in a header just for that purpose. This file commonly is named `gnome.h` and often holds these and other configuration values. The GTK+ and GNOME software development system has its makefiles automatically generate `config.h`. Also, it is possible to create the definitions using the `-D` option on the compiler’s command line.

The call to `bindtextdomain()` on line 20 relates the package name with the directory to be searched so any translation requests know where to look. The call to `textdomain()` on line 21 assigns the current application to the specified package.

The program creates two buttons, each of which has a text label. The first label is declared as a quoted string on line 45. The label is declared as it normally is, except that it is inside the braces of a macro with the name `_()`. The name of the macro is the underscore character; the underscore macro marks the string for translation. Created on line 49, the second button also has a translatable label, but this time a variable name is used. The underscore macro is still required, but because the string is defined elsewhere, there is one more step. The string is declared on line 13 and, because it needs to be marked as translatable, it is enclosed in another macro with a short name—the `N_()` macro.

That’s all there is to it. Make sure you mark all the strings that require translation (skipping those that don’t, as on lines 23 and 27). If all your strings are marked, and your application is translated into another language, they all are translated and inserted into the tables.

There is a drawback to writing translatable code. Your program is very limited in what it can do to create strings dynamically. If you don’t know the contents of a string at compile time, it cannot be translated. There is no way to read a string from a file, or from the user’s input, and have it translated for display. You can, however, combine untranslated strings with translated strings by using `printf()` or `sprintf()`. For example, say the translator finds this string in need of translation:

```c
"The last device in the list is %s\n"
```

This string can be translated, and will work just as you may expect, as long as the `%s` is left somewhere in the string. Things get a little more difficult if there are two variables in the string. For example:

```c
"Device number %d has been set to %s mode\n"
```

It can be translated, but the translator must take care that the `%d` and `%s` remain in the same order because that is the order the arguments appear on the function call.

## Summary

A wide range of environmental settings and controls can be stored in disk files and used to configure your program. This can include color settings, menu items, toolbars, and even the language. The principal items covered in this chapter were:

- Configuration settings can be made for each individual user, and can be made to apply to all users. There are also special provisions for security of configuration data.
- There is a standard API for saving and restoring configuration data. The data is stored as ASCII, but is converted to and from C data types inside the application.
- You can use the two pre-defined macros to mark text included in an application so it can be translated automatically into another language, depending on the environment in which the program is run.

This chapter completes the second, step-by-step, part of the book. The third part of the book contains information of a more general nature, such as a complete widget reference. The first chapter in the third part, Chapter 20, explains using `automake` and `autoconf` to automate compiling and linking.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_544_0.png)

# References and Mechanics

- **In This Chapter**
  - **Chapter 20:** Configuration and Compilation
  - **Chapter 21:** The Widgets of GTK+
  - **Chapter 22:** The Widgets of GNOME
  - **Chapter 23:** Some Linux Mechanics
  - **Chapter 24:** Comparative Anatomy: Win32 and GNOME

# Chapter 20: Configuration and Compilation

![](img/8bcc1ba72831c7d67cfc8b395deab95f_548_0.png)

This chapter provides a list of steps you can take to set up an applications development environment based on GNOME and GTK+.

There are hundreds of ways to set up a software development environment. The make files used throughout this book are simple and easy to use. However, because of their simplicity, they become unwieldy for a large project. Manually updating the make files can become difficult, and is prone to error.

There are any number of ways to automate the compile and link process, but GNOME has a semi-standard form it uses so it makes sense to copy these methods and use them for your GNOME applications.

Using this configuration, you still need to maintain some files by hand. But, once you get set up, there is surprisingly little to do to make changes and additions. For example, to change the version number of the system being compiled, you enter the new version number in one place and it automatically is inserted into the code of a header file. If you add a new source module, you enter its name in one place in one file. Consequently, all of its dependencies are determined and it is compiled in with the rest of the code.

## Install GNOME Source Code

For GNOME development, you need access to the GNOME source code. It is supplied as part of GNOME, so if you have GNOME installed, you probably already have the source installed.

## In This Chapter

- Installing your copy of the GNOME system source code
- Creating the autoconf and autogen scripts that can be used to create your make files
- Understanding the relationships among the scripts, your source code, and the make files
