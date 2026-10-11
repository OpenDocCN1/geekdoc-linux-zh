
Listing 18.1: continued

```c
153: * Skip tickers that are either
154: * unknown, or are producing parse
155: * errors in the returned data:
156: */
157: if ( tickers[x].flags & FLG_UNKNOWN
158:  || tickers[x].flags & FLG_ERROR )
159:     continue; /* Ignore this */
160:
161: /*
162: * Pick up the earliest "next" time:
163: */
164: if ( !tn
165:  || tickers[x].next_samp < tn )
166:    tn = tickers[x].next_samp;
167:
168: /*
169: * If the current time is >= than
170: * the "next" time, it is time to
171: * fetch an update for this ticker:
172: */
173: if ( td >= tickers[x].next_samp ) {
174:    /*
175:    * Get Quote Update:
176:    */
177:    z = get_tickinfo(
178:       &tickers[x], cmddopt_a);
179:
180:    /*
181:    * Compute time for the next
182:    * update for this ticker:
183:    */
184:    time(&tickers[x].next_samp);
185:    tickers[x].next_samp += tm;
186:
187:    /*
188:    * If the quote fetch was OK,
189:    * then broadcast its info:
190:    */
191:    if ( !z )
192:       broadcast(s, &tickers[x],
193:          (struct sockaddr *)&bc_addr,
194:          bc_len);
195: }
196:
197:
198: /*
199: * Here the interval between updates is
200: * progressively increased to 5 minutes
201: * max. This provides a lot of initial
202: * action for demonstration purposes,
203: * without taxing the friendly quote
204: * providers if this program is run all
205: * day. Abuse will only force the kind
206: * providers to change things to break
207: * the operation of this program!
208: */
209: if ( tm < (time_t) 5 * 60 )
210:    tm += 5; /* Progressively increase */
211:
212: /*
213: * Compute how long we need to snooze.
214: * The time to the next event is
215: * computed - sleep(3) is called if
216: * necessary:
217: */
218: if ( !tn )
219:    tn = td + tm;
220: if ( tn >= td )
221:    if ( zzz = tn - td )
222:       sleep(zzz);
223:
224:
225: return rc;
226:
227: /*
228: * Error Exit:
229: */
230: errxit:
231:    return rc = 2;
232: }
```

Note the following highlights about the program organization:

- This program accepts the -a or -b options, which are stored in variables cmdopt_a and cmdopt_b, respectively (lines 9 to 13).
- The stock market tickers to be monitored are maintained in the table tickers[] (line 18). The variable ntick indicates how many active entries are in the table (line 19).
- Function usage() provides usage information upon request when option -h is provided (lines 24 to 36).
- The remainder of the program is the main program for the server (lines 41 to the end).

Now, examine the flow of control in the server main program:

1. Options are parsed in a `getopt(3)` loop (lines 62 to 88).
2. The broadcast address is formed in `bc_addr` by calling upon the `mkaddr()` function (lines 94 to 106).
3. A UDP socket is created by calling `socket(2)` (lines 111 to 118).
4. Enable the broadcast feature of the socket from step 3 (lines 123 to 133).
5. Call upon the `load()` function to load the `tickers[]` table from the initialization file `tickers.rc` (lines 138 and 139).
6. The server then executes an infinite server loop until the program is terminated (lines 144 to 233).

Now, examine the server loop steps that are used:

1. The “next time” value `tn` is cleared to zero (line 145). The current time is also placed into `td` (line 146).
2. A for loop in line 151 iterates through all ticker table entries (lines 151 to 196). This loop will later be described separately.
3. The value of `tn` represents the time to pause between ticker updates. It was initialized to a value of 20 (seconds) in line 50. In line 209, it is tested to see whether the value is greater than five minutes. If not, `tm` has five more seconds added to it (line 210). This is done so that the time interval will increase gradually (to a maximum of five minutes), in case the server is left running all day. This will prevent abuse of the Yahoo! quotation servers, which are kindly providing a free service to you.
4. If an event time is found in `tn`, the amount of time to sleep is computed and placed into variable `zzz` and `sleep(3)` is called. Otherwise, the loop immediately begins another iteration.

Now examine the more interesting for loop beginning in line 151:

1. The ticker table entries contain a `flags` member. If the flag bit `FLG_UNKNOWN` is set (line 157), this indicates that the ticker has been discovered to be unknown. After this bit is set, the ticker is never looked up again (`continue` in line 159 causes it to be ignored). Likewise, if flag `FLG_ERROR` is set (line 158), the ticker is not looked up again. This flag indicates that a data format error was encountered while trying to decode the quotation.
2. The current time and date in `td` are compared with the next event time for the ticker entry `ticker(x)` (line 173). The next event time is stored in member `next_samp`, which indicates when the next sample should be taken. If the current time is greater than or equal to the next sample event time, then it is time to fetch a new quote for this ticker.
3. The function `get_tickinfo()` is called to obtain ticker information for this ticker symbol (lines 177 to 178).
4. A next event time is computed from taking the current time and adding the time period `tm` to it (which increases to a maximum of five minutes). This is done in lines 184 to 185.
5. A test is made to see whether the ticker quote fetch was successful (line 191). If it was, the function `broadcast()` is called in lines 192 to 194 to send the information out to all interested local area network client programs.
6. Repeat step 1, increasing `x`, until all ticker symbols have been processed in `tickers[]`.

That covers the operation of the main segment of the server code. The next sections will cover the operation of the quotation fetch and then the broadcast function.

### Fetching Quotations via `get_tickinfo()`

This section will examine the source module `getick.c` so that you can see how the quotation was retrieved by the C code. Before that module can be shown, however, you need to examine some of the structure references that are being used. Listing 18.2 shows the `quotes.h` header file used by the source modules in this project.

**Listing 18.2:** `quotes.h`—The `quotes.h` Header File

```c
1:    /* quotes.h:
2:    *
3:    *  Project header file:
4:    */
5:    #include <stdio.h>
6:    #include <unistd.h>
7:    #include <stdlib.h>
8:    #include <errno.h>
9:    #include <ctype.h>
10:   #include <string.h>
11:   #include <getopt.h>
12:   #include <memory.h>
13:   #include <stdarg.h>
14:   #include <math.h>
15:   #include <syslog.h>
16: #include <signal.h>
17: #include <sys/types.h>
18: #include <sys/time.h>
19: #include <sys/socket.h>
20: #include <netinet/in.h>
21:
22: /*
23:  * Default Quote Server:
24:  */
25: #define DFLT_SERVER "finance.yahoo.com:80"
26:
27: /*
28:  * Default Broadcast Address:
29:  */
30: #define DFLT_BCAST "127.255.255.255:9777"
31:
32: /*
33:  * CSV Parsing Parameter:
34:  */
35: typedef struct {
36: 	char 	type;	/* 'S' or 'D' */
37: 	void 	*parm;	/* Ptr to parameter */
38: } Parm;
39:
40: /*
41:  * Timeout on Quote Fetch:
42:  */
43: #define TIMEOUT_SECS 	10
44:
45: /*
46:  * Ticker load file:
47:  */
48: #define TICKPATH 	"tickers.rc"
49:
50: /*
51:  * Maximum number of tickers:
52:  */
53: #define MAX_TICKERS 	256
54:
55: /*
56:  * Ticker length:
57:  */
58: #define TICKLEN 	8
59:
60: /*
61:  * Date Length:
62:  */
63: #define DTLEN		10
64:
65: /*
66:  * Time field length:
67:  */
68: #define TMLEN		7
69:
70: /*
71:  * Define TRUE & FALSE if not defined:
72:  */
73: #ifndef TRUE
74: #define TRUE		1
75: #define FALSE		0
76: #endif
77:
78: /*
79:  * Ticker Request Structure:
80:  */
81: typedef struct {
82: 	char	ticker[TICKLEN+1];	/* Symbol */
83: 	double	last_trade;		/* Last Price */
84: 	char	*date;		/* Date */
85: 	char	*time;		/* Time of Last Trade */
86: 	double	change;		/* */
87: 	double	open_price;	/* Opening Price */
88: 	double	high;		/* High Price */
89: 	double	low;		/* Low Price */
90: 	double	volume;		/* Volume of Trades */
91: 	int	flags;		/* Server flags */
92: 	time_t	next_samp; /* Time of next evt */
93: } TickReq;
94:
95: /*
96:  * Ticker Flags:
97:  */
98: #define FLG_UNKNOWN		1	/* Ticker unknown */
99: #define FLG_ERROR		2	/* Data format error */
100:
101: /*
102:  * External Function References:
103:  */
104: extern int load(
105: 	TickReq *tick, int *pntick, int nmax);
```

![](img/961a0296fe36074690a9847b79332eff_501_0.png)
