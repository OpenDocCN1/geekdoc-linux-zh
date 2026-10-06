Line 3: Romeo, Romeo! wherefore art thou Romeo?
Finished processing the file
$

The while command loop continues processing lines of the file with the read command, until the read command exits with a non-zero exit status.

# Summary

This chapter showed three different methods for retrieving data from the script user. Command line parameters allow users to enter data directly on the command line when they run the script. The script uses positional parameters to retrieve the command line parameters and assign them to variables.

The shift command allows you to manipulate the command line parameters by rotating them within the positional parameters. This command allows you to easily iterate through the parameters knowing how many parameters are available.

There are three special variables that you can use when working with command line parameters. The shell assigns $ to the number of parameters entered on the command line. The $ * contains all of the parameters as a single string, and the $@ contains all of the parameters as separate words. These variables come handy when trying to process parameter lists.

Besides parameters, your script users can also use command line options to pass information to your script. Command line options are single letters preceded by a dash. Different options can be assigned to alter the behavior of your script. The bash provides three ways to handle command line options.

The first way is to handle them like command line parameters. You can iterate through the options using the positional parameter variables, processing each one as it appears on the command line.

Another way to handle command line options is with the getopt command. This command converts command line options into a standard format that you can process in your script. The getopt command allows you to specify which letters it recognizes as options and which options require an additional parameter value. The getopt command processes the standard command line parameters and outputs the options and parameters in the proper order.

The bash shell also includes the getopts (note that it is plural). The gets command provides more advanced processing of the command line parameters. It allows for multi-value parameters, along with identifying options not defined by the script.

The final method to allow data from your script users is the read command. The read command allows your scripts to interactively query users for information and wait. The read command