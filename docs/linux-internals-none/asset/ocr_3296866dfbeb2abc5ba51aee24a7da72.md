# Linux Kernel Base Functions



```
fflush(stderr);
for (i=1; i<6; i++) {
	/* This read will block */
	retval = read(fd, &data, sizeof(unsigned long));
	if (retval == -1) {
		perror("read");
		exit(errno);
	}
	fprintf(stderr, " %d",i);
	fflush(stderr);
	irqcount++;
}
fprintf(stderr, "\nAgain, from using select(2) on /dev/rtc:");
fflush(stderr);
for (i=1; i<6; i++) {
	struct timeval tv = {5, 0}; /* 5 second timeout on select */
	fd_set readfds;
	FD_ZERO(&readfds);
	FD_SET(fd, &readfds);
	/* The select will wait until an RTC interrupt happens. */
	retval = select(fd+1, &readfds, NULL, NULL, &tv);
	if (retval == -1) {
		perror("select");
		exit(errno);
	}
	/* This read won't block unlike the select-less case above. */
	retval = read(fd, &data, sizeof(unsigned long));
	if (retval == -1) {
		perror("read");
		exit(errno);
	}
	fprintf(stderr, " %d",i);
	fflush(stderr);
	irqcount++;
}
/* Turn off update interrupts */
retval = ioctl(fd, RTC_UIE_OFF, 0);
if (retval == -1) {
	perror("ioctl");
	exit(errno);
}
/* Read the RTC time/date */
retval = ioctl(fd, RTC_RD_TIME, &rtc_tm);
if (retval == -1) {
	perror("ioctl");
	exit(errno);
}
fprintf(stderr, "\n\nCurrent RTC date/time is %d-%d-%d, %02d:%02d:%02d.\n",
	rtc_tm.tm_mday, rtc_tm.tm_mon + 1, rtc_tm.tm_year + 1900,
```