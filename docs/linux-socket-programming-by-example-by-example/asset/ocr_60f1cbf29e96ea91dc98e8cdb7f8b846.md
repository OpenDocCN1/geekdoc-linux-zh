```
Listing 18.1: continued

15: */
16: * Ticker Table:
17: */
18: static TickReq tickers[MAX_TICKERS];
19: static int ntick = 0;
20:
21: */
22: * Return server usage information:
23: */
24: static void
25: usage(void) {
26: printf("Usage: %s [-h] -a address:port\n"
27: "where:\n"
28: "\t-t\tRequests usage info,\n"
29: "\t-a address:port\tSpecify "
30: "the server\n"
31: "\t\taddress and port number.\n"
32: "\t-b bcast:port\tSpecify "
33: "the broadcast\n"
34: "\t\taddress and port number.\n",
35: command);
36: }
37:
38: */
39: * Server Main Program:
40: */
41: int
42: main(int argc,char **argv) {
43: int rc = 0; /* Return Code */
44: int optch; /* Option Char. */
45: int z; /* Status Code */
46: int x; /* Index */
47: int s; /* Broadcast socket */
48: time_t tn = 0; /* Time Next */
49: time_t tzz; /* Sleep Time */
50: time_t tm = 20; /* Seconds */
51: time_t td; /* Time + Date */
52: struct sockaddr_in bc_addr; /* bc addr */
53: socklen_t bc_len; /* bc addr len. */
54: const int True = TRUE; /* Const. TRUE */
55: static char cmdopts[] = "ha:b:";
56: */
57: * Process command line options:
58: */
59: command = Basename(argv[0]);
60:
```