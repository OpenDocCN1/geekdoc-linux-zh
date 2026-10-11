# Modifying Scripts

If you modify scripts and add your own informational messages for output, you can either update an existing `doc/*.txt` file or create your own text file. Either way, you should update the `doc/explain.idx` (index) file afterward. The easiest way to do this is to create a new one by executing the following commands from the top-level `tiger` directory (we backed up the old index file first) as shown in Example 13-23.

# Example 13-23 Regenerating the `tiger` Explanation Database Index

```
# cp doc/explain.idx doc/explain.idx.old
# util/gensmsgidx doc/*.txt > doc/explain.idx
```

### `tiger` Source Files

There are some utilities in the `systems/Linux/2/` directory that create some of the files used by `tiger`. These are shown in Example 13-24.

# Example 13-24 `tiger` Configuration Helper Utilities

```
gen_alias_sets
gen_bootparam_sets
gen_cron
gen_export_sets
gen_group_sets
gen_inetd
gen_mounts
gen_passwd_sets
gen_services
```

The `util/buildconf` script generates the `config` script. If you are porting `tiger`, you may want to pay attention to the files in the lower half of Table 13.3 on page 348. Create a directory structure similar to an existing tree (such as `default`) under the `systems` directory, adding OS and/or release information as appropriate. You can generally get this information from the commands `uname -s` (for the system) and `uname -r` (for the version information). You may have to modify these scripts if the files on your system are in a different location.

# Adding New Checks

Scripts may be general—they will be run on every platform—or they may be written to run for a particular operating system, release, revision, or architecture.

To write a new general script, model the new script after an existing `tiger` script and place it in the scripts directory. For the most run-time flexibility, create a new variable for the `tigerrc` file. Edit the main `tiger` script and make it test the value of the variable in the `tigerrc` file (y or n). You can now run the script stand-alone, from `tiger`, or via `tigerrc`.

For system-specific checks, there are two approaches. The first method involves adding the commands to a script called `check` in the `systems` directory