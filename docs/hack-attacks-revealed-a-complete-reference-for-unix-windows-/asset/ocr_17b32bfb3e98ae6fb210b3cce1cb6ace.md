```
} 

/* Now, thisitem is first before/at boundary. */ 

good = netobuf; /* where the good bytes go */ 

while (nfrontp > thisitem) { 
if (ewant(thisitem)) { 
int length; 

next = thisitem; 
do { 
next = nextitem(next); 
} while (ewant(next) && (nfrontp > next)); 

length = next-thisitem; 
bcopy(thisitem, good, length); 
good += length; 
thisitem = next; 
} else { 
thisitem = nextitem(thisitem); 
} 
} 

nbackp = netobuf; 
nfrontp = good; /* next byte to be sent */ 
neturg = 0; 
} 

/* 
* netflush 
* Send as much data as possible to the network, 
* handling requests for urgent data. 
*/ 

netflush() 
{
int n; 

if ((n = nfrontp - nbackp) > 0) { 
/* 
* if no urgent data, or if the other side appears to be an 
* old 4.2 client (and thus unable to survive TCP urgent data), 
* write the entire buffer in non-OOB mode. 
*/ 
if (neturg == 0) || (not42 == 0)) { 
n = write(net, nbackp, n); /* normal write */ 
} else {
n = neturg - nbackp; 
/* 
* In 4.2 (and 4.3) systems, there is some question about 
* which byte in a sendOOB operation is the "OOB" data. 
* To make ourselves compatible, we only send ONE byte 
* out of band, the one WE THINK should be OOB (though
```

557