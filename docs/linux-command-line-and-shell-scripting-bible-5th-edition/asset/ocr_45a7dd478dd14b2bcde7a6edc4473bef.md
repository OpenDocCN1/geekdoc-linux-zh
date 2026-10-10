# # The gawk Program

The *gawk* program is the GNU version of the original *awk* program in UNIX. The *awk* program takes stream editing one step further than the *sed* editor by providing a programming language instead of just editor commands. This section describes the basics of the *gawk* program as a quick reference to its abilities.

# ## The gawk command format

The basic format of the *gawk* program is as follows:

*gawk* *options* *program* *file*

Table B.2 shows the options available with the *gawk* program.

**TABLE B.2 The gawk Options**

| Option | Description |
| :--- | :--- |
| -F fs | Specifies a file separator for delineating data fields in a line. |
| -f file | Specifies a filename to read the program from. |
| -v var=value | Defines a variable and default value used in the *gawk* program. |
| -mf N | Specifies the maximum number of fields to process in the data file. |
| -mr N | Specifies the maximum record size in the data file. |
| -W keyword | Specifies the compatibility mode or warning level for *gawk*. Use the help option to list all the available keywords. |

The command-line options provide an easy way to customize features in the *gawk* program.

# ## Using gawk

You can use *gawk* either directly from the command line or from within your shell scripts. This section demonstrates how to use the *gawk* program and how to enter scripts for *gawk* to process.

# ### Reading the program script from the command line

A *gawk* program script is defined by an opening and closing brace. You must place script commands between the two braces. Because the *gawk* command line assumes that the script is a single text string, you must also enclose your script in single quotation marks. Here’s an example of a simple *gawk* program script specified on the command line:

$ gawk ' {print $1}' 

This script displays the first data field in every line of the input stream.