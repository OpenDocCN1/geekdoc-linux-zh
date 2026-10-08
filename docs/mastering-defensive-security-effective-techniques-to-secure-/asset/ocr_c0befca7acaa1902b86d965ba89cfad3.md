The preceding figure shows that the bravo file has a + sign at the end of the permissions, which indicates that the file has an ACL.

# Managing ACLs

To set an ACL on a file, you can use the setfacl command.

In the following example, we show the syntax of the command in which we want to create an ACL for the bravo file to provide rwx permissions to the cesar user:

```
setfacl -m u:caesar:rw bravo
```

You can create ACLs for groups using g (groups) instead of u (user). In the following example, you can see how we are creating an ACL for the bravo file to add read and write permissions to the managers group:

```
setfacl -m g:managers:rw bravo
```

Now, let's explore more uses of the setfacl command.

# Default ACL on directories

When creating ACLs on directories, any files created within that directory will have default ACL inherit automatically.

To achieve this, we are going to use the same the setfacl command but with some different parameters. In this example, we are creating a default ACL for the bravito folder to provide read access to cesar:

```
setfacl -m default:u:caesar:r bravo
```

The following figure shows how the bravisimo inherits the permissions of the default ACL we just created for the bravisimo directory:

![](bbox=[0.237, 0.704, 0.719, 0.853])

Figure 7.21 – Default ACL on a directory