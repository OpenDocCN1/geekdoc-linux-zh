
## 6.6 Making a Tcl Object

```t
####################################################################
# proc addDirToTree
#   Add a directory to a node.
#   Create children for each directory entry, and set the
#   name and type of each child.
# Arguments:
#   parent The parent node for this directory.
#   directory The directory to add to the tree.
# Results:
#   The Tree is made longer by the number of entries in this
#   directory.

proc addDirToTree {parent newDir} {
#
  # If this isn't a directory, it has no subordinates.

if {[file type $newDir] != "directory"} {
    error "$newDir is not a directory. Can't add to tree."
}
#
  # If the parent directory hasn't been updated with name and
#   type, do so now.

if {[catch ($parent get name)]} {
    $parent set name $newDir
    $parent set type directory
}
#
  # An empty or unreadable directory will return a fail for
#   the glob command
#   If the directory can be read, the list of names will be in
#   fileList.

  set fail [catch (glob $newDir/**) fileList]
if {$fail} {
    return;
}
# Loop through the names in fileList
#
foreach name $fileList {
    set node [$parent add]
    $node set name $name
    $node set type [file type $name]
}
```

## Chapter 6. Procedure Techniques

### Example Script

```tcl
# Create a tree structure
#
set base [newTreeObject]
#
# Add the initial directory and its directory entries to the
# tree structure
#
addDirToTree $base [file filename C:/]
#
# If any children are directories, add their entries to the
# tree as sub-children.
#
foreach entry [$base childList] {
    if [[$entry get type] == "directory"] {
        addDirToTree $entry [$entry get name]
    }
}

# Print out the tree in the form:
# Dir1
# Dir1/Entry1
# Dir1/Entry2
# Dir2
# Dir2/Entry3
# Dir2/Entry4
```

```tcl
foreach entry [$base childList] {
    puts "[$entry get name]"
    if [[$entry get type] == "directory"] {
        foreach sub [$entry childList] {
            puts "[$sub get name]"
        }
    }
}
```

Script Output

- C:/IO.DOS
- C:/MSDOS.DOS
- C:/COMMAND.DOS
- C:/COMMAND.COM
- C:/BOOTLOG.PRV
- C:/CONFIG.SYS
- C:/NETLOG.TXT
- C:/DRVSPACE.BIN
- C:/AUTOEXEC.BAT
- C:/CONFIG.WIN
- C:/Program Files
    - C:/Program Files/Common Files
    - C:/Program Files/PLUS!
    - C:/Program Files/The Microsoft Network
    - C:/Program Files/Microsoft Exchange
    - C:/Program Files/Accessories
    - C:/Program Files/Tcl
    - C:/Program Files/Seagate
    - C:/Program Files/WinZip
- C:/tcltutor
    - C:/tcltutor/nopty.tcl
    - C:/tcltutor/icon
    - C:/tcltutor/TclTutor.bat
- C:/WINDOWS
    - C:/WINDOWS/INF
    - C:/WINDOWS/COMMAND
    - C:/WINDOWS/SYSTEM

The preceding example is very similar to the example in Chapter 5, since most of the code deals with the file system, not with the tree. However, it's a bit easier to follow with the shorter subcommand names used instead of the long tree procedures.

There are two problems with this tree object.

- 1. The associative array Tree_InternalArray sits at the global scope, where any code can access it easily.
- 2. The script that wishes to use the treeObject needs to know the directory where treeObj.tcl is stored, and treeObj.tcl needs to be able to find treeObj.tcl.

Chapter 7 will discuss the namespace and package commands. The examples show how to use the namespace command to hide the Tree_InternalArray in a private namespace and how to use the package command to create a package that can be used without the script needing to know the location of the files it loads.

## 6.7 Bottom Line

- A procedure can be defined as taking an undefined number of arguments by placing the args argument last in the argument list.
- A procedure argument with a default value is defined by declaring the argument as a list. The second list element is the default value.
- When a Tcl procedure is evaluated, it creates a local scope for variables. This local scope stacks below the scope of the code that invoked the procedure.
- A Tcl script can access all of the scopes above it in the procedure call stack.
- Tcl procedures can be constructed and evaluated in a running procedure.
- Data items can be treated as objects by creating a procedure with the same name as the data item and using that procedure to manipulate the data item.
- The rename command renames or removes a command or proc.
  Syntax: rename oldName ?newName?
- The subst command performs a pass of command and variable substitutions upon a string.
  Syntax: subst string
- The eval command will evaluate a set of arguments as a Tcl command.
  Syntax: eval arg ?args?
- The info commands command will return a list of commands that are visible in the current scope and match a pattern.
  Syntax: info commands pattern
- The info args command will return the arguments of a procedure.
  Syntax: info args procName
- The info body command will return the body of a procedure.
  Syntax: info body procName
- The global command declares that a variable exists in the global scope.
  Syntax: globalvarName ?varName2...varNameN

## Namespaces and Packages

The namespace and package commands help you write modular and reusable code in Tcl. These commands implement two different concepts that work together to make it possible to write more modular code. The namespace command lets you organize the code and data within...

## Chapter 7. Namespaces and Packages

This chapter will discuss:
- The namespace scope.
- Encapsulating procedures and data in namespaces.
- Nesting one namespace within another.
- Modularizing Tcl scripts into packages.
- Nesting packages within namespaces.

## 7.1 Namespaces and Scoping Rules

In Chapter 6 we discussed the global and procedure scopes. This section will expand on that and introduce the namespace variable. These commands allow the Tcl programmer to create private areas in which procedures will not conflict.

### 7.1.1 Namespace Scope

Namespaces provide encapsulation similar to that of C++ and other object-oriented languages. Namespace scopes have some characteristics of the global scope and some of procedure scope. A namespace can be viewed as a global scope.

Namespaces are similar to the global scope in that:
- Procedures created at any scope within a namespace are visible at the top level of the namespace.
- Variables created in a namespace scope (outside a procedure scope) are maintained between execution of code within the namespace.

### 7.1.2 Namespace and Scoping Rules

- Variables created in a namespace scope (outside a procedure scope) can be accessed by any procedure that is being evaluated within that namespace.
- While a procedure defined within a namespace is being evaluated, creates a local scope within that namespace, not within the global namespace.

Namespaces are similar to local procedure scopes in that:
- Code being evaluated within a namespace can access variables and procedures defined in the global space.
- All namespaces are contained within the global scope.
- Namespaces can nest within each other.

Namespaces also have some unique features:
- A namespace can declare certain items (procedures or variables) to be exportable. Exportable items can be made visible in the global scope.
- A nested namespace can keep procedures and variables hidden from higher level namespaces.

The following diagram shows the scopes in a script that contains two namespaces (example and demo), each of which contains procedures named proc1 and proc2. Because the procedures are in separate namespaces, they are different procedures. If a script tried to define two proc1 procedures at the global level, the second definition would overwrite the first.

In this example, example::proc1 and example::proc2 are procedures that are both called independently, while demo::proc2 is called from demo::proc1.
