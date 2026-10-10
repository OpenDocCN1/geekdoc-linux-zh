# ## CHAPTER
## 14

# # Handling User Input

# ## IN THIS CHAPTER

+   - Passing parameters
+   - Using special parameter variables
+   - Being shifty
+   - Working with options
+   - Standardizing with options
+   - Getting user input

So far you've seen how to write scripts that interact with data, variables, and files on the Linux system. Sometimes, you need to write a script that has to interact with the person running the script. The Bash shell provides a few different methods for retrieving data from people, including command-line parameters (data values added after the command), command-line options (single-letter values that modify the behavior of the command), and the capability to read input directly from the keyboard. This chapter discusses how to incorporate these various methods into your Bash shell scripts to obtain data from the person running your script.

# ## Passing Parameters

The most basic method of passing data to your shell script is to use *command-line parameters*. Command-line parameters allow you to add data values to the command line when you execute the script:

```
```
$ ./addem 10 30
```
```

This example passes two command-line parameters (10 and 30) to the *addem* script. The script handles the command-line parameters using special variables. The following sections describe how to use command-line parameters in your Bash shell scripts.

# ## Reading parameters

The Bash shell assigns special variables, called *positional parameters*, to all of the command-line parameters entered. This includes the name of the script the shell is executing. The positional