+   - -v    status files.
+       List version strings for performance tool files.
+   - -Z    Dump perstat info to a file and tar tape.

Using the `-c` option, you get information about your system configuration, as shown in the following listing:

```
# perfstast -c

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
\*\* perfstast for rp ux6 on Fri May 15 12:20:06 EDT
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

system configuration information:

uname -a: HP-UX ux6 B.11.00 E 9000/800 71763 8-user license

mounted file systems with disk space shown:
Filesystem          kbytes    used    avail %used Mounted on
/dev/vg00/lvol3     85016    27675  54736  34% /
/dev/vg00/lvol1     67733   44928  16031  74% /stand
/dev/vg00/lvol8    163840   56995  90927  42% /var
/dev/vg00/lvol7    497712  358775 132155  73% /usr
/dev/rp06vg tmp /tmp       4319777 1093927 3134084 26% /tmp
/dev/vg00/lvol6     270336  188902  76405  71% /opt
/dev/vg root1/ var   640691   15636  605834   3% /newvar
/dev/vgroot1/usr    486677  356866 115210  76% /newusr
/dev/vgroot1/stand  677733   45109  58580  74% /newstand
/dev/vgroot1/root    83733   21181  54178  28% /newroot
/dev/vgroot1/opt     263253  188109  67246  74% /newopt
/dev/vg00/lvol15     20480     119   8168   6% /home

LAN interfaces:
Name           Mtu        Network       Address       Ipkts     Opkts
lo0            4136      127.0.0.0     localhost     77442     77442
lan0           1500      192.60.11.0   rp-ux6       7847831   12939169

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
           (end of perfstast -c output)  \*\*\*\*\*\*\*\*\*\*\*\*\*\*
```

Using the `-f` option shows the size of the performance tools status files, as shown in the following listing: