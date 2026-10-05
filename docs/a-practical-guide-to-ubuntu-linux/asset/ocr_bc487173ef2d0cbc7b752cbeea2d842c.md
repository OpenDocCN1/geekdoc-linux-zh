# EXERCISES 367

Shell features There are several ways to customize the shell's behavior. You can use options on the command line when you call bash. You can use the bash set and shopt builtins to turn features on and off.

Command-line When it processes a command line, the Bourne Shell may replace some words with expanded text. Most types of command-line expansion are invoked by the appearance of a special character within a word (for example, a leading sign sign denotes a variable). Table 9-6 on page 326 lists these special characters. The expansions take place in a specific order. Following the history and all expansions, the common expansions are parameter and variable expansion, substitution, and pathname expansion. Surrounding a word with double quotation marks suppresses all types of expansion except parameter and variable expansion. Single quotation marks suppress all types of expansion, as does quoting (escaping) a special character by preceding it with a backslash.

# EXERCISES

+   1. Explain the following unexpected result:

$ where
date: /bin/date ...
$ echo $PATH
usr/local/bin:/usr/bin:/bin
$ cat > date
echo "This is my own version of date."
$ /date
Fri May 21 11:45:49 PDT 2010

+   2. What are two ways you can execute a shell script when you do not have execute permission for the file containing the script? Can you execute a shell script if you do not have read permission for the file containing the script?

+   3. What is the purpose of the PATH variable?
Set the PATH variable so that it causes the shell to search the following directories in order:
* /usr/local/bin
* /usr/bin
* /bin
* /usr/kerberos/bin
* The bin directory in your home directory
* The working directory