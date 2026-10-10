This example relies on subtle order effects: On the command line, standard error is redirected to standard output before standard output is redirected to /dev/null; however, bash interprets these redirections in the opposite order. Thus, this command will send nothing as input to `text2gif` if you reverse the order of the two redirection operators. Also, when redirecting to `&1` or `&2`, you should include no space between the redirection operator and its destination.

# ### Criteria for Completion

This task demonstrated the use of pipe and redirection operators for standard input, standard output, and standard error. You should now be able to apply these operators in working with Linux commands that generate textual output or expect textual input. (A few commands, such as `text2gif`, generate binary output on standard output and rely on you to be able to redirect or pipe it appropriately.)

# ## Task 1.8: Manage the Shell Environment

Linux shells are simply programs, and like many programs, the details of their operation can be customized. You can change the command prompt, set the directories in which the shell searches for program files, and so on. These features are adjusted via *environment variables*, which you can set on the command line or in configuration files. Other programs can also use environment variables, so in some cases, setting an environment variable in a `bash` configuration file can affect programs launched from `bash`.

# ### Scenario

You dislike your current `bash` prompt and want to change it to something that includes the date and time. You also need to set an environment variable that tells various programs what editor to use when calling an external text editor. You want to test these changes and then make them permanent by modifying your `bash` configuration file.

# ### Scope of Task

To perform this task, you'll need to type a few commands at the command line and edit a configuration file. Consult Task 1.5 for information on using Vi for file editing, or use your favorite text-based or GUI editor.

# ### Duration

This task will take about half an hour to complete. Once you know how to change environment variables, you'll be able to do so in under a minute—but it may take longer than that to determine what environment variable needs changing!