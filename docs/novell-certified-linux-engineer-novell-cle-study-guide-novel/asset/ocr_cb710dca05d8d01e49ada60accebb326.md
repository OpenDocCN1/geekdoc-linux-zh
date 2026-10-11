**device. Jumper 1 is assigned the value 1, jumper 2 is assigned the value 2, and jumper 3 is assigned the value 4. If you put a shunt on jumpers 2 and 3, the SCSI ID is set to 6. If you put a shunt only on jumper 1, the SCSI ID is set to 1. If you don't put shunts on any jumpers, the SCSI ID is set to 0.** Representing permissions in Linux numerically works in the same way.

If a permission is assigned, its value is added to the value of the respective digit. If it isn't assigned, a null value (0) is added to the value of the digit.
This can be a hard concept to understand for many Linux users. Let's look at a few examples.

Notice in Figure 3.11 that Owner has been assigned Read and Write permissions. Execute has not been assigned. The first digit in 644 represents Owner's permissions. The first digit is the sum of the values for the Read and Write permissions:

+   Read: 4
+   + Write: 2
+   + Execute: 0
+   = Permission 6

Also, notice that Group has been assigned only the Read permission.
Therefore, the value of the second digit is

+   Read: 4
+   + Write: 0
+   + Execute: 0
+   = Permission 4

The same applies to the value of the Others digit:

+   Read: 4
+   + Write: 0
+   + Execute: 0
+   = Permission 4

The result is the permission 644. Let's work through another example.
Suppose a file has a permission of 750. What permission has been assigned to each entity?

Let's look at the first permission, 7. The only way to get the value 7 is to assign all permissions, as shown here: