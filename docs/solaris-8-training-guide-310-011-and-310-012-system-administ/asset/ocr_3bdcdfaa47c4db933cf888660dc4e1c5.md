as possible. The low-speed printer would be reserved as a backup printer when the high-speed printer was in use.

Printer class names must be unique and can contain a maximum of 14 alphanumeric characters and underscores. You are not obligated to define printer classes. You should add them only if you determine that using printer classes would benefit the users on the network.

# STEP BY STEP

# 10.2 Defining Printer Classes

To define a printer class, follow these steps:

+   1. Log in as superuser or lp on the print server.
2. Define a class of printers by using the lpadmin command:
   `lpadmin -p <printer-name> -c <printer-class>`

The arguments for lpadmin are described in Table 10.5.

TABLE 10.5

lpadmin ARGUMENTS

| Argument | Description |
|---|---|
| `-p <printer-name>` | The name of the printer you are adding to a class of printers |
| `-c <printer-class>` | The name of a class of printers |

The specified printer is added to the end of the list in the class in the print server's /etc/lp/classes/<printer-class> file. If the printer class does not exist, it is created. Verify the printers in a printer class by using the lpstat command:

```
lpstat -c printer-class
```

In the following example, the command adds the printer luna to the class roughdrafts:

```
lpadmin -p luna -c roughdrafts
```