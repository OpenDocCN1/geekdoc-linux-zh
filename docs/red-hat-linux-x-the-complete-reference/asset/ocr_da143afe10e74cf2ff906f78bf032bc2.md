Table 20-6: xinetd Attributes

| Attribute | Description |
|---|---|
| include | Inserts the contents of a specified file as part of the configuration file. |
| includedir | Takes a directory name in the form of includedir /etc/xinetd.d. Every file inside that directory will be read sequentially as an xinetd configuration file, combining to form the xinetd configuration. |

# Disabling and Enabling xinetd Services

Services can be turned on and off with the **disable** attribute. To enable a service, you set the disable attribute to **no**, as shown here:

```
disable = no
```

You then have to restart **xinetd** to start the service.

```
# /etc/rc.d/init.d/xinetd restart
```