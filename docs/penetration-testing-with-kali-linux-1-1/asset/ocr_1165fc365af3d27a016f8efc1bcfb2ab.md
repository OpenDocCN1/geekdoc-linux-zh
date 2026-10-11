and the address of the 64-byte buffer variable where these characters will be copied (*dest* = **0065FE70**).

We can now step into the *strcpy* call (with *Debug* > *Step into* or F7). Notice that the addresses in the upper-left assembly instruction window have changed because we are now inside the *strcpy* function. This is noted by the highlighted address (**0x76485E90**) shown in Figure 195.

![](bbox=[0.12, 0.22, 0.9, 0.38])

Figure 195. Stack layout before *strcpy* execution

Now, we can double-click on the *strcpy* destination address (**0x0065FE70**) in the stack pane to better monitor the memory write operations occuring at that address. This address is highlighted in Figure 196 as noted by the red arrow:

![](bbox=[0.12, 0.48, 0.9, 0.65])

Figure 196. Monitoring the memory write operations

As shown in Figure 197, this changes the view of the stack pane slightly. Now, we see relative (positive and negative) offsets in the left-hand column instead of real addresses: