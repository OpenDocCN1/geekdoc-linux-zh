# Chapter 8 · The java.lang and java.util Packages

+   14. findDesiredProducts(map);
15. shipProducts(map);
16. printInvoices(map);
17. collectMoney(map);
18. }

Note the declaration of map on line 9. The reference type on the left-hand side of the sign is Map, not HashMap (the interface, rather than the class). This is a very important difference whose value will become clear later on. The processing methods do not concern us here. Just consider their declarations:

```
private void findDesiredProducts(Map map) { ... }
private void shipProducts(Map map) { ... }
private void printInvoices(Map map) { ... }
private void collectMoney(Map map) { ... }
```

Imagine that each of these methods passes the map to other subordinate methods, which pass it to other methods; our program has a large number of processing methods. Throughout the code, the argument types will be Map, not HashMap (again, the interface, rather than the class).

As development proceeds, it becomes clear that the getShoppers() method should return the Map's keys (which are the shoppers' e-mail addresses) in a sorted array. There are and will always be three shoppers, there are and will only be three keys to sort; the easiest implementation is as follows:

+   1. String[] getShoppers() { // New return type
2. Shopper sh1 = getNextShopper();
3. String email1 = getNextEmail();
4. Shopper sh2 = getNextShopper();
5. String email2 = getNextEmail();
6. Shopper sh3 = getNextShopper();
7. String email3 = getNextEmail();
8.
9. Map map = new HashMap();
10. map.put(email1, sh1);
11. map.put(email2, sh2);
12. map.put(email3, sh3);
13.
14. findDesiredProducts(map);
15. shipProducts(map);
16. printInvoices(map);
17. collectMoney(map);
18.