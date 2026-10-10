
## Adding Command-Line Options

A GNOME application can display a brief listing of all the arguments by using the `-usage` option this way:

```
% showoptions -usage
Usage: showoptions [-?V?] [--disable-sound] [--enable-sound]
    [--speaker=HOSTNAME:PORT] [-usage] [--gdk-debug=FLAGS]
    [--gdk-no-debug=FLAGS] [-display=DISPLAY] [-_sync]
    [-no-xshm] [-name=NAME] [-class=CLASS]
    [--xgid-host=HOST] [--xgid-port=PORT] [--xim-preedit=STYLE]
    [--xim-status=STYLE] [-gdk-debug=FLAGS]
    [--gtk-no-debug=FLAGS] [--g-fatal-warnings]
    [--gtk-module=MODULE] [-usage] [-sm-client-id=ID]
    [--sm-config-prefix=PREFIX] [--sm-disable]
```

You can add your own command-line options and have the system treat them the same way it does the built-in options. That is, your options are parsed from the command line and stored for your program to use them later. Also, they are listed on the help and `-usage` options along with the predefined options. This software is known as *popt*.

You define your options as an array of `poptOption` structs. Each member of the array is one option. The struct contains all the descriptive information for the option:

```c
struct poptOption {
  const char *longName;
  char shortName;
  int argInfo;
  void *arg;
  int val;
  char *descrip;
  char *argDescrip;
};
```

The `longName` and the `shortName` hold the characters that are expected on the command line. The long name is the one used with a pair of dashes, and the short name is the character used with a single dash. For example, a long name of *nocolor* and a short name of *n* allows the option to be specified on the command line as either *--nocolor* or *-n*.

The string `descrip` is a brief description of the argument. If it is specified, the string appears as the description when the `-help` option is used. The `argDescrip` string also is used in the description to show how the value is to be specified. For example, if an argument with the long name `border-color` has the `argDescrip` *COLOR*, the display in the output from `-help` is *--border-color*=*COLOR*.

The `argInfo` field defines the kind of argument and the data type of the value, if any, expected on the command line. Table 12-2 lists the possible values for `argInfo`. Table 12-3 lists the bit masks that you can use to set options for each of the argument types.

### Table 12-2: The Types of Arguments Known to Popt

| **Argument Type Name** | **Description** |
| :--- | :--- |
| `POPT_ARG_NONE` | The option is an on-off switch, so it does not require a value on the command line. |
| `POPT_ARG_STRING` | The value on the command line is in the form of a quoted string. |
| `POPT_ARG_INT` | The value on the command line is limited to the range of values of an `int`. |
| `POPT_ARG_LONG` | The value on the command line is limited to the range of values of a `long`. |
| `POPT_ARG_INCLUDE_TABLE` | This is not a command-line option. The `arg` pointer in the struct is the address of another `poptOption` array to be included. |
| `POPT_ARG_CALLBACK` | This is not a command-line option. The `arg` pointer is the address of a callback function that is to be used to parse the command-line options. This should be included at the beginning of the options array. |
| `POPT_ARG_INTL_DOMAIN` | The `arg` value is a pointer to a string defining the translation domain to be used with this table. |
| `POPT_ARG_VAL` | This is not a command-line option, although it can be used to set a default option. The location pointed to by `arg` should take on the value of `val`. |

### Table 12-3: Option Flags to Modify Popt Arguments

| **Option Name** | **Description** |
| :--- | :--- |
| `POPT_ARGFLAG_ONEDASH` | Allows a single dash to be used on the long name as well as the short name |
| `POPT_ARGFLAG_DOC_HIDDEN` | Suppresses the display of this option with the others by `--help` or `--usage` |
| `POPT_CFLAG_PRE` | Used with `POPT_ARG_CALLBACK` to call the callback before the parse |
| `POPT_CFLAG_POST` | Used with `POPT_ARG_CALLBACK` to call the callback after the parse |

This all may seem to be a bit more complicated than necessary, but the complications are necessary only when we are doing something very special with the arguments. In almost every case, it is simply a matter of creating an array of option descriptions, a place to store the input values, and a single function call. The following program defines and accepts five command-line arguments.

```c
1 /** readparm.c **/
2 #include <gnome.h>
3 
4 int toolbarParm = FALSE;
5 char *titleParm = NULL;
6 char *backgroundParm = NULL;
7 int widthParm = 100;
8 int heightParm = 50;
9 
10 struct poptOption opt[] = {
11   {
12     "title",'t',
13     POPT_ARG_STRING,
14     &titleParm,0,
15     "The text to appear on the title bar",
16     "TITLE"
17   },{
18     "width",'w',
19     POPT_ARG_INT,
20     &widthParm,0,
21     "The width of the window",
22     "WIDTH"
23   },{
24     "height",'h',
25     POPT_ARG_INT,
26     &heightParm,0,
27     "The height of the window",
28     "HEIGHT"
29   },{
30     "toolbar",'T',
31     POPT_ARG_NONE,
32     &toolbarParm,0,
33     "Display the toolbar",
34     NULL
35   },{
36     "background",'\0',
37     POPT_ARG_STRING,
38     &backgroundParm,0,
39     "The background color for the window",
40     "COLORNAME"
41   },
42   NULL,0,0,NULL,0,NULL,NULL
43 };
44
45 int main(int argc,char *argv[])
46 {
47  poptContext context;
48
49  gnome_init_with_popt_table("readparm","1.0",argc,argv,
50                              opt,0,&context);
51
52  g_print("toolbar: %s\n",
53          toolbarParm ? "TRUE" : "FALSE");
54  g_print("title: %s\n", titleParm ? titleParm : "NULL");
55  g_print("background: %s\n",
56          backgroundParm ? backgroundParm : "NULL");
57  g_print("width: %d\n",widthParm);
58  g_print("height: %d\n",heightParm);
59
60  poptFreeContext(context);
61  exit(0);
62 }
```

The declarations on lines 4 through 8 are the fields that receive the values entered on the command line. If an option does not appear on the command line, its value here is not changed; if you wish, you can store the default values in them, as this program shows with widthParm and heightParm.

Each parameter is defined as a member of the array of poptOption structs beginning on line 10. The first option, starting on line 12, requires a quoted string as its value on the command line and has both a long and short name. The long form can have an equal sign preceding the value. You can enter the argument in any of the following forms:

```
readparm --title "Title Text"
readparm --title="Title Text"
readparm -t "Title Text"
readparm --title TitleText
readparm --title=TitleText
readparm -t TitleText
```

The quotes are necessary only if the string contains blanks or if it begins with a hyphen (in which case, it could be confused with an argument tag). When the string is read from the command line, a pointer to it is stored in *titleParm* on line 5 because its address is specified in the table on line 14.

The height and width parameters defined on lines 18 through 28 are defined to return *int* data. The storage locations for the data are *widthParm* and *heightParm*, defined (with default values) on lines 7 and 8.

The toolbar argument defined on line 30 is a simple on-off switch. That is, there are no values associated with it on the command line. The program treats its presence or absence as a flag. The flag value, defined as *toolbarParm* on line 4, is an *int* with *FALSE* as its initial value. The value is changed to *TRUE* only if either *-toolbar* or *-T* is specified on the command line.

The argument defined on line 36 can be used to accept the name of a color as a string. The only way to use this argument is with the long form because the short form letter is the null character. A pointer to the name of the color is stored in *backgroundParm* defined on line 6.

All the arguments are read from the command line, parsed, converted into the appropriate data types, and stored in the specified fields with a single call to gnome_init_with_popt_table() on line 49. This call replaces the call to gnome_init() by adding three more parameters. The fifth argument is the address of the array of *poptOption* structs defining the parameters. The last argument is the address of a *poptContext* (which is itself a pointer) that receives the address of the descriptive *poptContext*. You can use this context to inquire about the options if more detailed information is required.

Memory is allocated to store the *poptContext*, so it probably should be returned to the system. However, it cannot be returned until you do not need the information stored in it any longer, such as any string arguments that were returned to you as pointers.

The parameters you define in your program are added to the list of those displayed. In this example, enter this command to see the parameters:

```
readparm --help
```

The output is the same list described above, with these added at the bottom:

```
readparm options
-t, --title=TITLE      The text to appear on the title bar
-w, --width=WIDTH      The width of the window
-h, --height=HEIGHT    The height of the window
-T, --toolbar          Display the toolbar
--background=COLORNAME The background color for the window
```
