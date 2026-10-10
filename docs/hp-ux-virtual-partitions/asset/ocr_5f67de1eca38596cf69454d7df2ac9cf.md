allowed, but some syntax forms are restricted to specific options, and some are only allowed once. Both are indicated in Table 1. In any case, resources in multiple specifications must not repeat or conflict with each other.

# Table 1. Resource syntax summary

| Resource | Forms | Options | # times/command |
|----------|-------|---------|-----------------|
| CPU | cpu:path | -a, -d | Multiple |
| | cpu:num | -a, -d, -m | Once |
| | cpu::[min:]max | -m | Once |
| I/O | io:path(:attr[;attr2]) | -a, -m, -d | Multiple |
| Memory | mem:size | -a, -m, -d | Once |
| | mem::base:range | -a, -d | Multiple |

Certain tasks can affect the outcome of others. To avoid errors, see the detailed description of the dependencies in the `vpresources(S)` manpage.

# RETURN VALUE

The `vparmodify` command exits with one of the following values:

+   - 0 Successful completion.
+   - 1 One or more error conditions occurred.

# EXAMPLES

Change the name of the virtual partition called Oslo to Bergen

```
`vparmodify -p Oslo -P Bergen`
```

Turn off the autoboost attribute for the virtual partition Oslo

```
`vparmodify -p Oslo -B manual`
```

Add two processors to the virtual partition Bergen in alternate database file /stand/Norway

```
`vparmodify -p Bergen -D /stand/Norway -a cpu:2`
```

# ERRORS

`vparmodify` displays error messages on stderr for any of the following conditions:

+   - An invalid option is specified.
+   - An invalid value is specified for an option or a value is omitted.
+   - The specified db_file does not exist, cannot be accessed, or has been corrupted.
+   - vp_name does not exist in the specified db_file or in the monitor database.
+   - new_vp_name already exists in the monitor database or specified db_file.
+   - vp_name is static and you have attempted to change a resource.