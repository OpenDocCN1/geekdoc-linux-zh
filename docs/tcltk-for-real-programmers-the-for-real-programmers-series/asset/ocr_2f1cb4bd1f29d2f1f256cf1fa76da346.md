# 7.3 A Tree Object Package with Namespaces

The next set of lines nests the tree namespace within the treeObject namespace.

The package require tree line causes the Tcl interpreter to search the pkgIndex.tcl files for information on how to load the tree package. When the source for the tree namespace is identified, those methods are stored in the auto_index variable.

As mentioned previously in this chapter, if we wait for the unknown procedure to be invoked to load the tree package automatically, it will be loaded at the global level, not nested within the treeObject package.

The next line, if `info auto_index::tree::treeCreate]`, tests to confirm that the expected indices into auto_index has been set. This index should be set. The only way for it not to be set for another tree package to be defined in your search path that doesn't have a treeCreate procedure defined.

If this index into auto_index exists, then a command script that will load the tree package (and resolve the undefined procedure tree-Create). It will resemble

```
source /usr/TclPackages/treeName.tcl
```

with a directory path that reflects where treeName.tcl is installed on your system.

The next line:

```
eval $auto_index::tree::treeCreate
```

evaluates the script and loads the tree package.

The last line in setting up the namespaces is to import the procedures from the tree namespace into the treeObject namespace. This is done with the command namespace import tree::*, which will import all the entities exported from tree. Note that these procedure names are being imported into the treeObject namespace, not into the global namespace. Importing into this space simplifies writing the treeObject code without polluting the global space.