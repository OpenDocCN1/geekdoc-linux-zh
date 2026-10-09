The **exec()** system call API extends the **fork()** system call by allowing you to call external programs and interact with them. This is essentially what CGI (Common Gateway Interface) calls are on the Web, as shown in the following:

+   - A host on the network offers a CGI server that takes a command. The command has command-line parameters typically in the following form:
	"http://www.server.com/cgi/\<command\>\?param1+param2+..."
- The client sends a message, for example
	"http://www.server.com/cgi/ls?tmp+proc"
- The server creates a child process and redirects the **stdin**, **stdout**, and **stderr** to the client's channel.
- Next the server calls the program using the **exec()** system call.

Notice the power of multitasking by the simple fact that running external programs cannot be done effectively without multitasking. The **exec()** system call comes in five flavors:

+   - **exec1()** Variable parameter list, first is the command with fully qualified path. All of the following parameters are the command-line arguments, beginning with the zeroth argument (**arg[0]**). The list ends with a zero or **NULL**.
	```c
	/* For example: */if ( exec1("/bin/ls", "/bin/ls", "-aF", "/etc", NULL)
	!= 0 )
	    perror("exec1 failed");exit(-1);    /* actually the "if" is redundant -
	                                             - exec does not
	                                             ↪return unless it failed */
	```
- **execl()** 's First Two Parameters

NOTE

The **exec1()** system call may appear redundant; Why are the first and second parameters the same command? The first parameter is the actual command name (to be executed), and the second is the zeroth command-line parameter (like **arg[0]** in **main()** of a C program). Don't forget to include the name—some external commands check the name to figure out what behavior to use. Also, don't forget the last **NULL** or zero; it indicates the end of the parameter list.

+   - **execp()** Similar to **exec1()**, but the command searches the execution path.
	```c
	/* For example: Find the program 'ls' in execution path */if (
	    execp("ls", "ls", "-aF",
	    "∂/etc", NULL) != 0 )    perror("execp failed");exit(-1);
	```
- **execle()** Similar to **execl()**, but the last parameter is an array of strings representing the environment. Remember to end the list of parameters with a **NULL** or zero.
	```c
	/* For example: */char *env[]={ "PATH=/bin:/usr/bin", "USER=gonzo",
	                                ∂NULL};
	if ( execle("/bin/ls", "/bin/ls", "-aF", "/etc", NULL, env) != 0 )
	    perror("execle failed");exit(-1);
	```
- **execv()** Has two parameters. The first is the fully qualified path of the command. The second is an array of command-line arguments. The last entry in the array is a zero or **NULL**.