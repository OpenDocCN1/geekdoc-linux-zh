```
if (ch != '\377') {
 *pfrontp++ = ch;
 }
 break;
}

/*
 * Check for urgent data...
 */
case DM:
 SYNChing = stilltoob(net);
 settimer(gotDM);
 break;

/*
 * Begin option subnegotation...
 */
case SB:
 state = TS_SB;
 continue;

case WILL:
 state = TS_WILL;
 continue;

case WONT:
 state = TS_WONT;
 continue;

case DO:
 state = TS_DO;
 continue;

case DONT:
 state = TS_DONT;
 continue;

case IAC:
 *pfrontp++ = c;
 break;
}
 state = TS_DATA;
 break;

case TS_SB:
 if (c == IAC) {
 state = TS_SE;
 } else (
 SB_ACCUM(c);
 }
 break;

case TS_SE:
```