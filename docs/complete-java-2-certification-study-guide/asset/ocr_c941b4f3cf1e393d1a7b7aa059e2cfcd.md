# The Collections Framework 281

```
19.   // New sorting code.
20.   String[] sortedKeys = new String[3];
21.   if (email1.compareTo(email2) < 0 &&
22.       email1.compareTo(email3) < 0) (
23.           sortedKeys[0] = email1;
24.           if (email12.compareTo(email3) < 0)
25.               sortedKeys[1] = email2;
26.           else
27.           sortedKeys[2] = email3;
28.     )
29.   else if (email2.compareTo(email3) < 0) (
30.       sortedKeys[0] = email2;
31.       if (email1.compareTo(email3) < 0)
32.           sortedKeys[1] = email1;
33.           else
34.               sortedKeys[2] = email3;
35.     )
36.   else {
37.       sortedKeys[0] = email3;
38.       if (email1.compareTo(email12) < 0)
39.           sortedKeys[1] = email1;
40.       else
41.           sortedKeys[2] = email2;
42.   }
43.   return sortedKeys;
44. }
```

The added code is fairly lengthy: 26 lines.

> Beware of specs claiming that the size of anything is and always will be small.

![](bbox=[0.118, 0.696, 0.223, 0.73])

Predictably, as soon as the code is developed and debugged, someone will decide that the program needs to be expanded to accommodate 20 shoppers instead of the original three. The new requirement suggests the need for a separate sorting algorithm, in its own separate method. The new method will be called sortString(). We won't list it here, but you can imagine that it involves a couple of loops and a lot of comparison and a bit of swapping array members. The next evolution of getShoppers() looks like this:

+   1. private String[] getShoppers() {
2.   String[] keys = new String[20];
3.   Map map = new HashMap()