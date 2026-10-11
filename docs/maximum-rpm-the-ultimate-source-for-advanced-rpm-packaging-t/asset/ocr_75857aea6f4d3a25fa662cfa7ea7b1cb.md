The following tags are all the ones defined at the time this book was written. For the latest list of available **queryformat** tags, issue the following command:

```
rpm --querytags
```

Keep in mind that the list of tags produced by the `--querytags` option is the complete list of all tags used by RPM internally (for instance, during package builds). Because of this, some tags do not produce meaningful output when used in a `-–queryformat` format string.

# # D.1. List of - -queryformat Tags

For every tag in this section, there can be as many as three different pieces of information:

+   - A short description of the tag.
+   - Whether the data specified by the tag is an array, and, if so, how many members are present in the array.
+   - What modifiers can be used with the tag.

# ## The NAME Tag

The NAME tag is used to display the name of the package.

Array: No

Used with modifiers: N/A

# ## The VERSION Tag

The VERSION tag is used to display the version of the packaged software.

Array: No

Used with modifiers: N/A

# ## The RELEASE Tag

The RELEASE tag is used to display the release number of the package.

Array: No

Used with modifiers: N/A

# ## The SERIAL Tag

The SERIAL tag is used to display the serial number of the package.

Array: No

Used with modifiers: N/A