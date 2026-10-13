# Deleting an existing service

To remove an existing service from a run level, use the following command:

```
chkconfig --del service_name [--level runlevel]
```

For example,

```
chkconfig --del named
```

removes the named service from the current run level. To remove the service from a different run level than the current one, use the --level option. For example,

```
chkconfig --del named --level 5
```

removes the named service from run level 5.

# Using ntsysv to manage run levels

The ntsysv utility enables you to turn on and off various services in any run levels, using a simple menu interface. When you run the command without any argument, it displays a screen similar to the one shown in Figure 2-1.

![](bbox=[0.1, 0.76, 0.7, 0.9])

Figure 2-1 The ntsysv screen