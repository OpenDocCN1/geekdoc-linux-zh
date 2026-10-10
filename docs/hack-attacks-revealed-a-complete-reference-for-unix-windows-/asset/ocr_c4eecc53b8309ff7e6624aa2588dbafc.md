```
if (SB_GET() != TELQUAL_IS) {
	return;   /* ??? XXX but, this is the most robust */
}

terminaltype = terminalname+strlen(terminalname);
while ((terminaltype < (terminalname + sizeof terminalname-1)) &&
		   !SB_EOF()) {
	register int c;

	c = SB_GET();
	if (isupper(c)) {
		c = tolower(c);
	}
	*terminaltype++ = c;   /* accumulate name */
}
*terminaltype = 0;
terminaltype = terminalname;
break;

}

	default:
		;
}

mode(on, off)
	int on, off;
{
	struct sgttyb b;

	ptyflush();
	ioctl(pty, TIOCGGETP, &b);
	b.sg_flags |= on;
	b.sg_flags &= ~off;
	ioctl(pty, TIOCSETP, &b);
}

/*
 * Send interrupt to process on other side of pty.
 * If it is in raw mode, just write NULL;
 * otherwise, write intr char.
 */
interrupt()
{
	struct sgttyb b;
	struct tchars tchars;

	ptyflush();   /* half-hearted */
	ioctl(pty, TIOCGGETP, &b);
	if (b.sg_flags & RAW) {
		*pfrontp++ = '\0';
		return;
	}
```