# 1.5 Tcl as an Embeddable Interpreter

restricted system access to an unsigned applet (called a ticklet in Tcl), partial access to a ticklet from a slightly trusted source, or ActiveX-style full access to an applet that is encrypted with a key you truly trust.

+   - Smaller downloadable objects. Because the Tcl libraries live on the machine where an application runs, there is less to download with a Tcl/Tk application than a similar set of functionality written in Java.

# 1.4 Tcl as an Extensible Interpreter

Many programming groups these days have a set of legacy code, a set of missions, and a need to perform some sort of rapid development. Tcl can be used to glue these code pieces into new applications.

Using Tcl, you can take the existing libraries and turn them into commands within a Tcl interpreter. Once this is done, you'll have a language that you can use to develop rapid prototypes or even shippable programs.

Merging the existing libraries into the interpreter gives you a chance to hide sets of conventions that may have grown over several years and projects and expose the application programmer to a consistent application interface (API).

This technique gives you a chance to graft a graphics interface over older, non-GUI-based sets of code.

# 1.5 Tcl as an Embeddable Interpreter

Programs frequently start as a simple proof of concept with hardcoded values. These values quickly evolve into variables that can be set with command lines. Shortly after that, the command lines get unruly, and someone adds a configuration file and a small interpreter to parse the configuration. The macro language then grows to control program flow as well as variables. Then it starts to get messy.