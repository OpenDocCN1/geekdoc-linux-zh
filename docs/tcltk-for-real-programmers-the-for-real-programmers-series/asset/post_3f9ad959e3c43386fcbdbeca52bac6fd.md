
## Chapter 7. Namespaces and Packages

enhanced, and new features added, but code that worked with a previous
minor revision should work with later minor revisions.

- The revision numbers are compared integer by integer. Revision 2.0 is
more recent than revision 1.99.

## 7.2.5 Package Cookbook

### 7.2.5.1 Creating a Package

- Create the Tcl file or files. You can split your package procedures
across several files if you wish.

- Add the command

```
package provide packageName versionNumber
```

to the beginning of these Tcl source files.

- Invoke tclsh. If you have several revisions of Tcl installed on your system,
be certain to invoke the correct tclsh. The package command was intro-
duced with 7.6 and was modified slightly in Tcl 8.0 and Tcl 8.1.

- At the % prompt, type

```
pkg_mkIndex directory fileNamePattern ?Pattern2...?
```

You may include multiple file names in this command. The pkg_mkIndex
command will create a new file named pkgIndex.tcl with information
about the files that were listed in the pkg_mkIndex command.

### 7.2.5.2 Using a Tcl Package

- If the package is not located in one of the Tcl search directories listed by
default in the auto_path variable, you must add the directory that con-
tains the package's pkgIndex.tcl file to your search list. This can be
as follows:

```
append auto_path /usr/project/packageDir
```
in the beginning of your Tcl script.

- Set the environment variable TCLLIBPATH to include your package
directory. The environment variable need not include the path to the
default Tcl library.

## 7.3 A Tree Object Package with Namespaces

- Add your package directory to the auto_path definition in the init.tcl file. This file will be located in the Tcl library directory.
The location of that directory is an installation option.

- Add the line
```
package require packageName ?versionNumber?
```
in the beginning of your script.

- If you need the package to load immediately, follow the package require command with
```
global auto_index # if this is within a procedure
eval $auto_index(packageProcedureName)
```
There is more discussion about why this eval command is needed in the next section.

## 7.3 A Tree Object Package with Namespaces

This section will describe how to turn the tree.tcl and treeObject.tcl scripts we've developed into a pair of scripts that implement a tree object package with most of the commands protected within namespaces.

### 7.3.1 Adding Namespace and Package to tree.tcl

The first step in this process is to make the procedures defined within the tree.tcl file into a package with the procedures and variables enclosed within a namespace.

The beginning code for tree.tcl (which had been a set of Tcl procedure definitions) now looks like this:

#### Example 7.3.1-1

```
package provide tree 1.0
namespace eval tree {
# Export the public entry points
namespace export treeCreate treeChild treeDestroyTree \
treeDeleteNode
```

namespace export treeGetChildList treeGetParent treeSetNodeValue
namespace export treeNodeValue treeGetNodeList \
treeGetRoot treeDump
namespace export treeSetValue treeGetTreeView \
treeGetTreeViewList
namespace export treeGetSiblingList

# Tree_InternalArray is the array in which all nodes and trees
# reside.
# It is a persistent data object, shared among all procedures
# within this namespace.

variable Tree_InternalArray

# Initialize the base counter.

set Tree_InternalArray(base) 0;

```tcl
# proc treeCreate() {
    variable Tree_InternalArray;
    #
    # Create the unique name for this tree.
    set primaryName "tree$Tree_InternalArray(base)"
    incr Tree_InternalArray(base)
    #
    # Set the initial unique ID for nodes in this tree.
    #
    set Tree_InternalArray($primaryName.base) 0;
    #
    # Create the root node
    #
    set rootNode [TreeCreateNode $primaryName.base]
    #
    # Looks good, ship it!
    #
    return $rootNode
}
```

## 7.3 A Tree Object Package with Namespaces

The package provide tree 1.0 line informs Tcl that this file defines the tree package, revision level 1.0.

The namespace eval tree evaluates all the following code as being within the tree namespace. This includes all of the procedure definitions and the Tree_InternalArray variable that had previously been maintained in the global namespace.

The namespace export commands allow the entry points to be accessed (and namespace imported) by other programs. The pkg_mkIndex command will put only exported names into the pkgIndex.tcl file; thus, any procedure that can be called from code outside the package should be listed here. Note that the internal tree procedure TreeGetNameParts is not listed here.

The Tree_InternalArray is declared to be a namespace variable with the variable Tree_InternalArray command. This line is not required. Defining a value for Tree_InternalArray would be sufficient. I prefer to make an explicit declaration.

Next, the base unique value for defining trees is set, and the treeObject namespace. If the TreeInternalArray were left global, instead of being changed to variable, the code would still work, but we would not gain the encapsulation.

## 7.3.2 The Tree Object in a Namespace

Putting a namespace around the tree object is a bit trickier. By nesting the tree within the treeObject namespace, the tree object will be isolated from other packages that might also use the same names.

The package provide tree 1.0 line informs Tcl that this file defines the tree package, revision level 1.0.

The namespace eval tree evaluates all the following code as being within the tree namespace. This includes all of the procedure definitions and the Tree_InternalArray variable that had previously been maintained in the global namespace.

The namespace export commands allow the entry points to be accessed (and namespace imported) by other programs. The pkg_mkIndex command will put only exported names into the pkgIndex.tcl file; thus, any procedure that can be called from code outside the package should be listed here. Note that the internal tree procedure TreeGetNameParts is not listed here.
