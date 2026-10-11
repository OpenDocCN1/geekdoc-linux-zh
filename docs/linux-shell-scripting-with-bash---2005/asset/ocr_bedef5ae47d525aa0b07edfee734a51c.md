# ## The Linux Execution Environment

As mentioned in the later section on exporting variables, when a Linux program runs, it doesn't start with an “empty state,” but inherits any variables exported by the previous program. Exported variables are called environment variables because they become part of the environment in which the new program is running.

Variables are not the only things exported by the original program. The environment consists of:

+   - Open files
+   - The current working directory
+   - The file creation mode *umask*
+   - Any signal handlers set by *trap*
+   - Exported environment variables
+   - Exported shell functions
+   - Options enabled at invocation (either by default or with command-line arguments) or by *set*
+   - *shopt* shell options
+   - Shell aliases
+   - Various process IDs, including those of background jobs, the value of `$$_`, and the value of `$PPID`

Subshells inherit their environment from the parent scripts. The environment of a subshell consists of:

+   - Open files (possibly modified by redirections to the subshell)
+   - The current working directory
+   - The *umask* value
+   - Shell variables marked for export
+   - Signal traps

Like environment variables, the process of exporting open files, the working directory, or traps is one way. If the new program decides to close standard output, it closes only its copy of the original program's standard output. The original program cannot be affected by the actions of the new program. The entire environment acts the same way.

# ## The Source Command ( . )

When one script is executed by another, all variables, aliases, and other items declared in the script are lost when the second script completes its run. Results can be returned only by files, by standard output, or by the script's status code.