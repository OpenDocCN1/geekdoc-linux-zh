
## 6.3 Getting Information about Procedures

These four info subcommands will return information about the procedures that have been defined:

- info commands `pattern`
Return a list of commands with names that match a pattern.

- info procs `pattern`
Return a list of procedures with names that match a pattern.

- info body `procName`
Return the body of a procedure.

- info args `procName`
Return the arguments of a procedure.

The commands subcommand will list the available commands that match a glob pattern. This command is useful when you are debugging code that runs in several namespaces (discussed in Chapter 7) and you need to know what commands are defined where.

**Syntax:** `info commands` `pattern`

- info commands
Returns a list of commands in the local and global scope that match the pattern.

- `pattern` 
nA glob pattern to attempt to match.

The `info body` command will return the body of a procedure. This can be used to generate and modify procedures at run time and when debugging scripts that generate new procedures while they are running.

**Syntax:** `info body` `procName`

- info body Returns the body of a procedure.

- `procName` The procedure from which the body will be returned.

The `info args` command returns the argument list of a procedure. Again, this is useful when debugging code that has generated its own procedures.

**Syntax:** `info args` `procName`

- info args Returns a procedure's argument list.

- `procName` The procedure from which the arguments will be returned.

# Chapter 6. Procedure Techniques

The next example shows how you can check that a procedure exists create a slightly different procedure from it.

# Example 6.3-1

# Example Script

```
# Define a simple procedure.
proc alpha {args} {
    puts "proc alpha is called with these arguments: $args"
}
# Confirm that the procedure exists
if {[[info commands alpha] != ""} {
    puts "There is a procedure named alpha"
}
# Get the argument list and body from the alpha procedure
set alphaArgs [info args alpha]
set alphaBody [info body alpha]
# Change the word "alpha" in the procedure body to "beta"
regsub "alpha" $alphaBody "beta" betaBody
# Create a new procedure "beta" that will display its arguments.
proc beta $alphaArgs $betaBody
# Run the two procedures to show their behavior
alpha How 'bout
beta them 'Cubs.
```

# Script Output

There is a procedure named alpha
proc alpha is called with these arguments: How 'bout
proc beta is called with these arguments: them 'Cubs.

## 6.4 Substitution and Evaluation of Strings

## 6.4 Substitution and Evaluation of Tcl interpreter

Section 4.2 discussed how the Tcl interpreter evaluates a script: the interpreter examines a line, performs a pass of command and variable substitutions, and then evaluates the resulting line. A Tcl script can access these interpreter functions to perform substitutions on a string or even evaluate a string as a command. This is one of the unusual strengths in Tcl programming. Most interpreters do not allow access to their parsing and evaluation sections to the program that is being interpreted.

The two commands that provide access to the interpreter are subst and eval.

## 6.4.1 Performing Substitution on a String

The subst command performs a single pass of variable and command substitutions on a string and returns the modified string. This is the first phase of a command being evaluated, but the actual evaluation of the command does not happen. If the string includes a square-bracketed command, the command within the brackets will be evaluated as part of this substitution.

The subst command can be used when you need to replace a variable with its contents but do not want to evaluate it as a command. The following example shows how subst can be used to combine the contents of two variables into a variable name.

Syntax: subst string

subst Perform a substitution pass upon a string. Do not evaluate the results.

string The string upon which to perform substitutions.

# Example 6.4.1-1

# Example Script

```
% set x var
var
% set y name
name
% set varname "this is the test"
```

## 6.4.2 Evaluating a String as a Tcl Command

```
this is a test
% puts $(x)$(y)
$varname
% subst $(x)$(y)
this is a test
```

The eval command concatenates its arguments into a string and then evaluates that as if it were text in a script file. The eval command allows a script to create its own command lines and evaluate them.

You can use eval to write data-driven programs that effectively write themselves based on the available data. You can also use the eval command to write agent-style programs, where a task on one machine sends a program to a task on another machine to execute. These techniques (and the security considerations) will be described as they come up in the next chapters.

Syntax: eval arg args?

| command | description |
| :--- | :--- |
| eval | Evaluate the arguments as a Tcl script. |
| arg args? | These arguments will be concatenated into a command line and evaluated. |

The next example evaluates several lines of text to increment a variable.

# Example 6.4.2-1

Example Script

```
set cmd(0) {set a 1}
set cmd(1) {puts "start value of A is: $a"}
set cmd(2) {incr a 3}
set cmd(3) {puts "end value of A is: $a"}
```

```
for {set i 0} {$i < 4} {incr i} {
    eval cmd($i)
}
```

## 6.5 Working with Global and Local Scopes

Script Output
start value of A is: 1
end value of A is: 4

## 6.5 Working with Global and Local Scopes

The Tcl scope rules and their relation to the upvar and uplevel commands can be confusing. This section will discuss scopes and the upvar and uplevel in a bit more detail than they've been discussed previously and show how uplevel commands behave.

This discussion will be expanded again in Chapter 7, when we discuss the namespace command. For now, a namespace is a technique for encapsulation and variable names.

## 6.5.1 Global and Local Scope

The global scope is the primary scope in a Tcl script. All Tcl commands and procedures that are not defined within a namespace are maintained in this scope. All namespaces and procedures can access commands and variables maintained in the global scope.

Any variable declared global or outside a procedure is maintained in the global scope. Variables maintained in the global scope are kept until the script exits or they are explicitly destroyed with the unset command. These variables can be accessed from any other scope by declaring the variable to exist in the global scope with the global command. Note that the global command must be evaluated before that variable name is used in the local scope. The Tcl interpreter will generate an error if you try to declare a variable to using it in a local scope.

```
set globalVar "I'm global"
```

```
proc goodProc {
  global globalVar

# The next line prints out
#The globalVar contains: I'm global
puts "The globalVar contains: $globalVar"

proc badProc() {
  set globalVar "This 'globalVar' in the local scope"

  # The next line causes an error
  globalVar


When a procedure is evaluated, it creates a local scope. Variables are created in this scope as necessary and are destroyed when the procedure returns. The variables used within a procedure are visible to other procedures called from it but not to procedures outside the current stack.

When a new procedure is defined within a procedure, the new procedure is defined in the global scope and is not deleted when the procedure that defines the new procedure returns.

Each time a procedure invokes another procedure, another local scope is created. These nested procedure calls can be viewed as a stack, with the global scope at the top and each successive procedure call stacked below the previous ones.

A procedure can access variables within the global scope or within the scope of the procedures that invoked it via the upvar and uplevel-commands. The upvar command will link a local variable to one in a previous (higher) stack scope.

# Example 6.5.1-1

# Example Script

```
proc top {topArg} {
  set localArg [expr $topArg+1]
  puts "Before calling bottom localArg is: $localArg"
  bottom localArg
  puts "After calling bottom, localArg is: $localArg"
}

proc bottom {bottomArg} {
```