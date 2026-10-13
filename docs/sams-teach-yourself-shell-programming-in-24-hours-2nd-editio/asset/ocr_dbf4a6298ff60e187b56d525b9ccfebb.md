Here you replied yes to the question. You can confirm that the delete worked as follows:

```
$ ./showperson sriranga
$
```

Because there is no output from showperson, you know that this entry has been deleted.

# Summary

This chapter covered using shell scripts to solve two problems:

+   - Creating init or startup scripts
+   - Maintaining an address book

In the first example, you learned how the system boots and how scripts are used to streamline this process. In the second example, you developed three scripts that modify and view the contents of an address book. Some of the highlights of these scripts are

+   - The showperson script showed you how the grep and awk commands can be used to format input.
+   - The addperson script showed you how a single script can be used in both interactive and non-interactive modes.
+   - The delperson script showed you how to use the grep command and file descriptors to update a file accurately.

The examples in this chapter demonstrate how you can apply the tools covered in previous chapters to solve real problems. Using these scripts as examples, you can see some of the techniques used to solve everyday problems.

The next chapter explores several methods of writing scripts to ensure that they are portable between different versions of UNIX.

# Questions

1. Add a check to the sshd init script that verifies if the user is root. (Init scripts should only be executed by root.)
HINT: Use the id and sed commands.

2. The showperson script lists all matching entries in the address book based on a name provided by the user. The matches produced are case sensitive. How can you change the script matches so they aren't case sensitive?