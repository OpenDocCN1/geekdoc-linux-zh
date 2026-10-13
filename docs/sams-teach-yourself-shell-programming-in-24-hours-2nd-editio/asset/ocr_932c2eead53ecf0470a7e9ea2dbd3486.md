# Problems with the echo Command in Prompts

Most programs that need to prompt the users need to be able to print a prompt that is not terminated by a newline. In Chapter 5, "Input and Output," there were several problems with using the \c escape sequence of the echo command to do this. The workaround was to use the /bin/echo command.

Although this works for UNIX versions based on System V, on some BSD-based systems this does not work. You need to specify the -n option to echo instead. By using the following shell script, you can create a shell function, echo_prompt, to display a prompt reliably across all versions of echo:

```
_ECHO=/bin/echo
_N="-n"
_O="-c"
ECHOTEST=`$ECHO "hello \c"`
if [ "$ECHOTEST" = "hello \c" ] ; then
  _N="-n"
  _O=""
fi
export _ECHO_N_C
echo_prompt() { $_ECHO $_N $0 $_C ; }
```

This script fragment uses the /bin/echo workaround as the base from which to construct the correct echo command. It checks the output of an echo command to determine whether the \c sequence is handled correctly. If it is not, the -n option is enabled.

After the appropriate values have been determined, the function echo_prompt is created using these values. This function enables you to reliably output prompts on every system.

# Abstraction

Abstraction is a technique used to hide the differences between the versions of UNIX inside shell functions. By doing this, the overall flow of a shell script is not affected. When a function is called, it makes a decision as to what commands to execute.

You will learn about two different examples of abstraction:

+   - Adapting the getSpaceFree function to run on HP-UX
+   - Adapting the getPID function to run on both BSD and System V

This section uses the functions getOSName and isOS, given earlier in this chapter.

# Adapting getSpaceFree for HP-UX

Recall the getSpaceFree function introduced in Chapter 21:

```
getSpaceFree() {
  if [ $# -lt 1 ] ; then

```