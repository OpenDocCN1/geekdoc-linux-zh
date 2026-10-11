# Examining the Client Program

```
```
170:     a_len = sizeof adr; /* Max addr len. */
171:     z = recvfrom(s,              /* Socket */
172:             dgram,       /* Receiving buffer */
173:             sizeof dgram, /* Max rcv buf size */
174:             0,           /* Flags: no options */
175:             (struct sockaddr *)&adr,  /* Addr */
176:             &a_len);     /* Addr len, in & out */
177:
178:     if ( z < 0 ) {
179:             fprintf(stderr,
180:                     "%s: recvfrom(2)\n",
181:                     strerror(errno));
182:             break;
183:     }
184:
185:     /*
186:      * Extract and report quote:
187:      */
188:     if ( lextract(dgram,&tkr) ) {
189:             printf("%.8s %7.3f %s %7.3f %7.3f "
190:                    "%7.3f %7.3f %9.0f\n",
191:                    TICKLEN,
192:                    tkr.ticker,
193:                    tkr.last_trade,
194:                    tkr.date,
195:                    tkr.time,
196:                    tkr.change,
197:                    tkr.open_price,
198:                    tkr.high,
199:                    tkr.low,
200:                    tkr.volume);
201:             fflush(stdout);
202:     }
203:
204:     }
205:     return 0;
206: }
```
```

The interesting features of this program are as follows:

+   1.  Command-line options are parsed (lines 81 to 100).
+   2.  A broadcast address is formed (lines 105 to 118).
+   3.  A datagram (UDP) socket is created (lines 123 to 129).
+   4.  The SO\_REUSEADDR option is enabled (lines 135 to 146). This is essential if more than one client program is to receive the same broadcasts on the same host machine.