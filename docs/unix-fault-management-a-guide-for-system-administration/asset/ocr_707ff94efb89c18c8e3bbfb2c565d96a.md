```
scf ("%s",target);
now = temp.tv_sec;
while ( pstat_getproc(pst,sizeof (struct pst_status),
	1,index) > 0) {
	if (strcmp(target,pst.pst_ucomm)==0) {
	duration = now - pst.pst_start;
	convert_status(status,pst.pst_stat);
	printf ("PID %8d Status: %s\n",pst.pst_pid,status);
	printf ("Started %d seconds ago\n",duration);

	printf ("Real pages(DATA %d TEXT %d STACK %d)\n",
		pst.pst_dsize,pst.pst_tsize,pst.pst_ssize);
	printf ("RSS %d MAX RSS(hwm) %d\n",
		pst.pst_rssize,pst.pst_maxrss);
	printf ("Number of swaps: %d\n",pst.pst_nswap);
	}
	index = pst.pst_idx+1;
} /* end while loop */

printf ("Overall System Info:\n");
pstat_getstatic(mystatic,sizeof(struct pst_static),
	0,0);
pstat_getdynamic(dyn,sizeof(struct pst_dynamic),
	0,index);
printf ("Run queue len(1- %1f,",
	dyn.psd_avg_1_min);
printf ("5- %1f,",
	dyn.psd_avg_5_min);
printf ("15- %1f)\n",
	dyn.psd_avg_15_min);
printf ("Physical Memory: %d\n",mystatic.physical_memory);
printf ("Active Real Memory: %d Free pages: %d bytes\n",
	dyn.psd_arm,dyn.psd_free*mystatic.page_size);
}
```

# Listing 7-3	Program output showing pstat information.

```
# ./pstate
Enter process name:memhog
PID	24549 Status: running
Started 247 seconds ago
Real pages(DATA 1955 TEXT 3 STACK 3)
RSS 1979 MAX RSS(hwm) 1979
Number of swaps: 0
Overall System Info:
Run queue len(1- 0.000000,5- 0.000000,15- 0.000000)
Physical Memory: 393216
Active Real Memory: 0 Free pages: 0 bytes
#
```