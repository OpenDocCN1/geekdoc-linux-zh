```
>h_addr[1], (char)
		dest_he->h_addr[2], (char) dest_he->h_addr[3]); /* <-- ip&#42482;
	*/

#ifdef MYDEBUG
	for (length = 0; length < 8; length++)
		printf ("%02X:", (unsigned char) buffer[length]);
	printf ("\n");
	for (length = 0; length < 8; length++)
		if (buffer[length] > 'A' && buffer[length] < 'z')
		printf (" %c:", (unsigned char) buffer[length]);
	else
		printf (" *:");
	printf ("\n");

#endif

	/* error checking sucks */
	send (outsocket, buffer, 9, 0);
	recv (outsocket, buffer, 8, 0);

	/* handle errors etc */
	if (buffer[1] == 0x5B)
	send (insocket, portclosed, sizeof (portclosed), 0);
	#endif
	for (length = 0; length < 8; length++)
		printf ("%02X:", (unsigned char) buffer[length]);
	printf ("\n");
	for (length = 0; length < 8; length++)
		if (buffer[length] > 'A' && buffer[length] < 'z')
		printf (" %c:", (unsigned char) buffer[length]);
	else
		printf (" *:");
	printf ("\n");
#endif

	maxfd = insocket>outsocket?insocket:outsocket;
	while (1)
	{
		FD_ZERO (&rfds);
		FD_SET (insocket, &rfds);
		FD_SET (outsocket, &rfds);
		select (maxfd+1, &rfds, NULL, NULL);
		if (FD_ISSET (insocket, &rfds))
		{
			length = recv (insocket, buffer, sizeof (buffer), 0);
			if (length == -1 || length == 0)
			break;
			if ((send (outsocket, buffer, length, 0)) == -1)
			break;
		}
		if (FD_ISSET (outsocket, &rfds))
		{
			length = recv (outsocket, buffer, sizeof (buffer), 0);
			if (length == -1 || length == 0)
```