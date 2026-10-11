```
70: addresses[x].ip[1],
71: addresses[x].ip[2],
72: addresses[x].ip[3],
73: class,
74: netmask);
75: }
76: ;
77: return 0;
78: ;
```

The operation of this demonstration program can be summarized in the following steps:

+   1.  The socket address structure *addr inet* is defined in line 15. This will be the address that will be examined for classification.

+   2.  The addresses to be tested are defined in a static array of structures, defined in lines 20 to 27. You might want to experiment by trying other address numbers in lines 23 to 26.

+   3.  Line 29 starts a loop that will iterate through four entries in the *addresses* array. The subscript value will be the variable *x*.

+   4.  A socket address is initialized in lines 34 to 39, from *addresses[x]*. This is done in the same manner it was presented in the last chapter, and should look familiar to you now.

+   5.  The most significant byte is extracted out of the socket address *addr inet* in line 47. You will remember that the most significant byte is the first byte of the address, in network byte order (big-endian). With this byte lifted from the socket address, it will be possible to classify the address based upon the high-order bits in this byte.

+   6.  The *if* statement in line 50 tests to see whether the high-order bit is zero (review Figure 3.1, looking at the class A address). If the high-order bit is zero, you know you have a class A address (lines 51 and 52 execute).

+   7.  The *if* statement in line 53 tests to see whether the high-order bit is 1, and the 2nd highest bit is 0 (review the class B address in Figure 3.1). If this is true, then the statements in lines 54 and 55 classify this address as class B.

+   8.  The *if* statement in line 56 tests to see whether the highest two bits are 11 (binary), followed by a 0 bit. If this is true, then lines 57 and 58 classify the address as a class C address (review Figure 3.1 for class C addresses).