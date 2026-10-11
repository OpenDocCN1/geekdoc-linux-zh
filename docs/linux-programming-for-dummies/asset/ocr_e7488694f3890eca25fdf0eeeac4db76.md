I can, of course, include multiple destination addresses, multiple copy addresses, and multiple blind-copy addresses, plus a subject line by placing them on the same line.

# Inserting all features in an e-mail

You can include a subject, a copy address, and a blind copy in an e-mail by using all the switches that I mention in the preceding sections of this chapter. Simply insert the switches after the destination address as you call the mail utility.

The following example shows you how to do so:

```
mail bob@mycomputer -s "Promotions" -b boss@mycomputer -c mary@mycomputer < memo1
```

The mail utility sends Bob, Mary, and the boss memo1 and identifies the subject as Promotions.

![](bbox=[0.07, 0.49, 0.94, 0.78])