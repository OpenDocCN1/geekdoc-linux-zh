# 492 Chapter 14 Making Your Job Easier with Scripts

john|mary|terri|leonard|jacob|geoffrey|eric
tom|jeff|mike|larry|moe|curly|harpo

To cut out the name of the person responsible for the fourth day of weeks 1 and 2, you'd use this command:

```
cut -"d"| -f4 filename
leonard
larry
```

The cut command has several options to provide for actions besides cutting by whole fields. You can cut specific bytes, characters, or fields. You've seen that fields are specified by the -f parameter. To designate the retrieval of bytes, use -b; and for characters, use -c. To indicate the inclusion of all data between the nth byte, field, or character and the end of the line, add a hyphen character ( - ) after the number, and as in the following examples:

```
cut -"d"| -f4- filename
leonard|jacob|geoffrey|eric
larry|moe|curly|harpo
```

To indicate the inclusion of all data between the nth byte, field, or character and the nth byte, field, or character, use N-M as shown here:

```
cut -"d"| -f4-6 filename
leonard|jacob|geoffrey
larry|moe|curly
```

Finally, to indicate all the data on a line up to and including the nth byte, field, or character, precede the name with a hyphen ( - ) as shown here:

```
cut -"d"| -f-4 filename
john|mary|terri|leonard
tom|jeff|mike|larry|moe
```

Now that you have a basic idea of how to use the cut command, let's look at an example that's particularly suited to Linux system administration. Say, for example, that you need to set a variable to your IP address in a script. You can cut the value from the output of /sbin/ifconfig like this:

```
ip_address = /sbin/ifconfig ppp0 | grep inet | cut -d\': -f2 | cut
--d = " * -f1
```

![](bbox=[0.267, 0.931, 0.928, 0.948])