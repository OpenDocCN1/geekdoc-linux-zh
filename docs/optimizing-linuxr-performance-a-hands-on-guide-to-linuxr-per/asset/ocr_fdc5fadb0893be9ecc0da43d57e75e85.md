# 8.1. Performance Tool Helpers

Linux has a rich heritage of tools that can be used together and become greater than the sum of the parts. Performance tools are no different. Although performance tools are useful on their own, combining with other Linux tools can significantly boost their effectiveness and ease of use.

# 8.1.1. Automating and Recording Commands

As mentioned in an earlier chapter, one of the most valuable steps in a performance investigation is to save the commands that are issued and results that are generated during a performance investigation. This allows you to review them and look for new insights. With this, Linux provides the tee command, which enables you to save output to a file, or the script command, which records every key press and output displayed on the screen. This information can be saved and reviewed later or to create a script to automate test execution.

It is important to automate commands because it reduces the chance of errors and enables you to think about the problem without having to remember all details. Both the bash and the watch command enable you to periodically and automatically execute long and complex command lines after typing them. After you have the command line correct, bash and watch can periodically execute the command without the need to retry it.

# 8.1.2. Graphing and Analyzing Performance Statistics

In addition to the tools for recording and automation, Linux provides powerful analysis tools that help you understand the implications of performance statistics. Where most performance tools generate statistics as text output, it is not always easy to see patterns and trends over time. Linux provides the gnumeric spreadsheet, which can import, analyze, and graph performance data. When you graph the data, the cause of a performance problem may become apparent, or it may at at least open up new areas of investigation.

# 8.1.3. Investigating the Libraries That an Application Uses

Linux also provides tools that enable you to determine which libraries an application relies on, as well as tools that display all the functions a given library provides. The ldd command provides the list of all shared libraries that an application uses. This can prove helpful if you are trying to find the number and location of libraries that an application uses. Linux also provides the objdump command, which enables you to search through a library or application to display all the functions that it provides. By combining the ldd and objdump commands, an application can take the output of ltrace, which provides only the names of the functions that an application calls, and determine which library a given function is.

# 8.1.4. Creating and Debugging Applications

Finally, Linux also provides tools that enable you to create performance-friendly applications, in addition to tools that enable you to interactively debug and investigate the attributes of running applications. The GNU prof collection (gcc) can insert debugging information into applications that aid opprofile in finding the exact line and source file of a specific performance problem. In addition, the GNU debugger (gdb) can also be used to find information about running applications not available by default to various performance tools.