In the following example, the our devices are 1A20-1A24 (use your own values and do not type the angle brackets):

```
==> att <1a20-1a24> *
1a20-1a24 ATTACHED TO MAINT
```

**Important:** The angle brackets (<>) in our examples throughout the book mean that you should replace the our example values with the correct values for your site. For instance, if you are installing z/VM onto DASD 1200-1204, you would type the following:

==> att 1a00-1a04 *

# Running INSTDVD

The INSTDVD EXEC copies the z/VM system from DVD to disk. To run INSTDVD:

+   1. Execute the INSTDVD EXEC command:

```
==> instdvd
```

If you are using 3390-3s, a panel requests the five volumes (Figure 4-13).

![](bbox=[0.3, 0.6, 0.85, 0.8])

Figure 4-13 The instdvd DASD window

+   a. Enter the addresses of the five volumes on which z/VM will be installed.

+   b. Do not select the DO NOT FORMAT DASD check box on the right side of the panel.