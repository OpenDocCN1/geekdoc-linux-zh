```
amflag = 'a';
if (hour > 12)
{
    hour -= 12;
    amflag = 'p';
}
printf("%-11.11s <DIR>   %02d-%02d-%02d %2d:%02d%c\n",
    fffblk.ff_name,day,month,year,hour,min,amflag);
done = findnext(&ffblk);
}

/* Now all files except directories */
done = findfirst("*.*",&ffblk,231);

while (!done)
{
    year = ((ffblk.ff_fdate >> 9) + 80;
    month = ((ffblk.ff_fdate >> 5) & 0x0f;
    day = ffblk.ff_fdate & 0x1f;
    hour = ((ffblk.ff_ftime >> 11);
    min = ((ffblk.ff_ftime >> 5) & 63;

    amflag = 'a';

    if (hour > 12)
    {
        hour -= 12;

        amflag = 'p';
    }

    parsfnm(ffblk.ff_name,&fcb,1);

    printf("%-8.8s  %-3.3s  %8ld %02d-%02d-%02d  %2d:%02d%c\n",
        fcb.fcb_name,fcb.fcb_ext,ffblk.ff_fsize,
        day,month,year,hour,min,amflag);
    done = findnext(&ffblk);
}
```

The function parsfnm() is a Turbo C library command, which makes use of the DOS function for parsing an ASCII string containing a filename into its component parts. These component parts are then put into a DOS file, control block (fcb), from where they may be easily retrieved for display by printf(). The DOS DTA is composed as follows:

| OFFSET | LENGTH | CONTENTS |
| :--- | :--- | :--- |
| 00 | 15 | Reserved |
| 15 | Byte | Attribute of matched file |