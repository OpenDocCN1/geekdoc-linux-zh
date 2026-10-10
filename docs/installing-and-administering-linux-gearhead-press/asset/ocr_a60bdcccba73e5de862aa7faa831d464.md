# 162    Installing and Administering Linux 2E

tions are performed in the order in which they appear (in other words, from left to right). Example 6.2, which deals with the use of symbolic parameters to change permission modes, will illustrate what we mean.

When you use the symbolic mode to specify permissions, the first set of parameters you specify set the permission field, as follows:

+   * u file owner (when discussing permissions, owner permissions are often referred to as user)
+   * g group
+   * o all others
+   * a owner, group, and all others

Using `a` is the same as specifying the `ugo` option. The `a` option is the default permission field. That is, if you omit the permission field, Linux defaults to the `a` option.

The second set of flags determines whether permissions are to be added, taken away, or set as specified:

+   * `+` adds the specified permissions.
+   * `-` removes the specified permissions.
+   * `=` clears the selected permission field and sets it to whatever follows on the command line. If you do not specify a permission mode following the `=`, then Linux will remove all permissions from the selected field.

The third set of parameters determines the permission as shown here:

+   * r read permission
+   * w write permission
+   * x execute permission for files; search permission for directories

To change permissions, you should first issue the `ls -1` command to check the current permission settings (that is, the current file mode). Then, you use the `chmod` command to specify the symbolic modes. Finally, it is a good idea to check these new permissions by issuing the `ls -1` command again. This procedure is followed in Example 6.2.

> **NOTE** With symbolic and numeric notation, you do not separate entries with spaces. This situation is contrary to your experience with entering commands thus far.