**Listing 18.4: continued**

```
```
24:		cp += strlen(cp) + 1;
25:		strcpy(cp, quote->date);
26:		cp += strlen(cp) + 1;
27:		strcpy(cp, quote->time);
28:		cp += strlen(cp) + 1;
29:		sprintf(cp, "\xE", quote->change);
30:		cp += strlen(cp) + 1;
31:		sprintf(cp, "\xE", quote->open_price);
32:		cp += strlen(cp) + 1;
33:		sprintf(cp, "\xE", quote->high);
34:		cp += strlen(cp) + 1;
35:		sprintf(cp, "\xE", quote->low);
36:		cp += strlen(cp) + 1;
37:		sprintf(cp, "\xE", quote->volume);
38:		cp += strlen(cp) + 1;
39:
40:		msglen = cp - buf;
41:		/*
42:		 * Broadcast the datagram:
43:		 */
44:		z = sendto(s, buf, msglen, 0, bc_addr, bc_len);
45:		if ( z == -1 )
46:			msgff( 'e', "%s: sendto(2)\n",
47:				strerror(errno));
48:	}
```
```

The **broadcast**() function uses the following basic steps:

+   1.  The buffer **buf**[\*2048\*] is used to format the broadcast datagram (line 14). Pointer variable **cp** is used to build this datagram in stages (line 15).
+   2.  Line 21 starts building the datagram by copying the null terminated ticker symbol into **buf**[1]. A new pointer for **cp** is computed to point after the null byte that follows the ticker symbol in **buf**[1] (line 22).
+   3.  The last \_trade value is formatted and placed after the null byte in the datagram (line 23). Again, **cp** is computed to point past the null byte that follows (line 24).
+   4.  Lines 25 to 38 repeat this procedure for all other data components to be placed into the datagram. Note that each component is a null-terminated string unto itself, within this datagram.
+   5.  The final length of the datagram is computed (line 40) and stored into **msglen**.