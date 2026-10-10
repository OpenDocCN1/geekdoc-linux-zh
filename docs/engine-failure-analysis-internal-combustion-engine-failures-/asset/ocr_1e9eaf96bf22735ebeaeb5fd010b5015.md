new top directory current. Specify a directory to add a directory to the top of the stack and make this directory current.

See also dirs, pop.

# **OPTIONS**

**Use This Option** | **To Do This**
--- | ---
`+n` | Cycle the directory stack so that the nth directory is at the top
`-n` | Cycle the directory stack so that the nth directory from the bottom of the stack is at the top

# **EXAMPLES**

**This Command** | **Does the Following**
--- | ---
`pushd /home/suzanne/essays` | Adds the specified directory to the top of the stack and switches to this directory.
`pushd` | Switches the position of the top two directories on the stack and switches to the top directory. You can use this command to switch back and forth between two directories at the top of the stack.

# **slocate**

```
`slocate [ option ] [ shell pattern ]`
```

Quickly locates files by searching a database of filenames rather than the actual directory tree. Unlike **locate**, **slocate** is secure because it does not enable users to view files belonging to other users. By default, **slocate** uses a substring search, so it is not necessary to use