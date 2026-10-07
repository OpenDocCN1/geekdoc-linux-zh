# Chapter 17: Using Server APIs

much easier (see Chapter 12). You can read about the configuration files in Chapter
4 and Appendix B of the Programmer's Guide.

# DEFINING THE API

The Netscape API (which is called the "server plug-in API") is a set of functions
and header files that help you create functions with the directives in server
configuration files. The NetscapeTrack server uses this API to create the func-
tions for the directives used in magnus.conf (the server configuration file) and
obj.conf (the object configuration file). These built-in functions are described in
Appendix B of the FastTrack Administrator's Guide.

To write a new plug-in function for the FastTrack server, follow these steps:

+   1. Learn about the process the server uses to handle browser requests (see
   Chapter 4 in the Programmer's Guide).
2. Write the code for your plug-in functions. Each function applies to a
   specific directive in the configuration files.
3. Compile your code into a shared object file (.so file).
4. Include your shared object filename in the Init directives of the obj.conf
   configuration file.
5. Specify the directives and values that apply to your functions somewhere
   in the server configuration file (obj.conf).

# WRITING FUNCTIONS

The easiest to start writing a new function is to use the sample code in the
/nsapi subdirectory (under /opt/fasttrack after you've installed FastTrack on
OpenLinux). Exploring the sample code, the header files, and a makefile will
you understand how to start your own project.

The following subdirectories are included for you to review and use as you create
your functions:

+   * nsapi/examples/ : contains example C files for each function class you
  create
* nsapi/include/ : contains all the header files you include when writing
  your functions
* nsapi/include/base : contains header files for low-level, platform-
  independent functions such as file, memory, and network access
* nsapi/include/frame : contains header files for functions like server and
  HTTP-specific things, accessing the configuration files, and defining
  interaction with HTTP actions