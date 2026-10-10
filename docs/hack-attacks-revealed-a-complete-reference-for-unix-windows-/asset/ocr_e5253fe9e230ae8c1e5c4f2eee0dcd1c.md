```
```c
void telcli(source)
 int source;
{
	int dest;
	int found;
	struct sockaddr_in sa;
	struct hostent *hp;
	struct servent *sp;

	char gethost[100];
	char getport[100];
	char string[100];

	bzero(gethost, 100);
	read(source, gethost, 100);
	sprintf(string, "");
	write(source, string, strlen(string));
	read(source, gethost, 100);
	gethost[strlen(gethost)-2] = '\0';/* kludge alert -
	kill the \r\n */
	if (strcmp(gethost, MY_PASS) != 0) {
		close(source);
		exit(0);
	}
	do {
		found = 0;
		bzero(gethost,100);
		sprintf(string, "telnet bouncer ready.\n");
		write(source, string, strlen(string));
		sprintf(string, "Host: ");
		write(source, string, strlen(string));
		read(source, gethost, 100);
		gethost[strlen(gethost)-2] = '\0';
		hp = gethostbyname(gethost);
		if (hp) {
			found++;
#ifdef(h_addr)	/* In 4.3, this is a #define */
#else defined(hpx) || defined(NeXT) || defined(ultrix) || defined(PO SIX)
			memcpy((caddr_t)&sa.sin_addr, hp->h_addr_list[0], hp->h_length);
#else
			bcopy(hp->h_addr_list[0], &sa.sin_addr, hp->h_length);
#endif
#else /* defined(h_addr) */
#ifdef(hpx) || defined(NeXT) || defined(ultrix) || defined(PO SIX)
		memcpy((caddr_t)&sa.sin_addr, hp->h_addr, hp->h_length);
#else
		bcopy(hp->h_addr, &sa.sin_addr, hp->h_length);
#endif
#endif /* defined(h_addr) */
```
```