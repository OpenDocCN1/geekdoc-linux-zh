and one or more of the following modifiers:

+   - **A** Suppresses absolute filenames
+   - **l** Gives an error message if a link can’t be resolved
+   - **L** Follows symbolic as well as hard links
+   - **m** Doesn’t restore modification times (everything gets current date/time)
+   - **p** Extracts using the original permissions
+   - **v** verbose-tar is quiet by default
+   - **w** Waits for confirmation before each action
+   - **f** The next argument is the device name to use

These are the most important of the **tar** options, and they behave pretty much consistently across a variety of platforms. There may well be specific options appropriate to your particular situation or implementation of **tar**, so check with your system administrator if in doubt.

The final argument for **tar** is the files to be archived. This can be specific files or directories, or **tar** can be part of a piped command line if the device is "-" for standard input or output.

# Can I use tar to copy files to a different machine or filesystem?

Since tar follows subdirectories, it is easy to use for transferring complete directory structures to a different place. If, for example, you wanted to copy files to a new place, keeping everything intact, you could use

```
`cd sourcedir; tar cf - . | (cd targetdir; tar xf -)`
```

which would copy everything from the source directory to the target directory. It’s important that you use the dot for the source directory here so that the archive is created with relative path names. Use absolute path names for **sourcedir** and **targetdir** to avoid copying files to the wrong location.