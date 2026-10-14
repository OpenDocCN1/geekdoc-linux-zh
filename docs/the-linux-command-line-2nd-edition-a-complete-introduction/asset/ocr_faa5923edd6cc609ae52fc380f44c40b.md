A better way is to use the mktemp program (not to be confused with the mktemp standard library function) to both name and create the temporary file. The mktemp program accepts a template as an argument that is used to build the filename. The template should include a series of “X” characters, which are replaced by a corresponding number of random letters and numbers. The longer the series of “X” characters, the longer the series of random characters. Here is an example: tempfile=$(mktemp /tmp/foobar.$$.XXXXXXXX) This creates a temporary file and assigns its name to the variable tempfile. The “X” characters in the template are replaced with random letters and numbers so that the final filename (which, in this example, also includes the expanded value of the special parameter $$ to obtain the PID) might be something like: /tmp/foobar.6593.U02uvM6654 For scripts that are executed by regular users, it may be wise to avoid the use of the /tmp directory and create a directory for temporary files within the user’s home directory, with a line of code such as this: [[ -d $HOME/tmp ]] || mkdir $HOME/tmp

# Asynchronous Execution

It is sometimes desirable to perform more than one task at the same time. We have seen how all modern operating systems are at least multitasking if not multiuser as well. Scripts can be constructed to behave in a multitasking fashion.

Usually this involves launching a script that, in turn, launches one or more child scripts that perform an additional task while the parent script continues to run. However, when a series of scripts runs this way, there can be problems keeping the parent and child coordinated. That is, what if the parent or child is dependent on the other, and one script must wait for the other to finish its task before finishing its own?

bash has a builtin command to help manage asynchronous execution such as this. The wait command causes a parent script to pause until a specified process (i.e., the child script) finishes.

# wait

We will demonstrate the wait command first. To do this, we will need two scripts, a parent script: