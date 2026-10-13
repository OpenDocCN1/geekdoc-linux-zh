page, so answer c is incorrect. Because pw=/var/spool/lpd/lp0/70 is in an incorrect format for this command, answer d is incorrect.

# Question 7

Based on the following entry from the /etc/printcap file, where is the remote printer? You are located on the nicenetwork.rgb domain.

```
lp|lr2|Color Laser:rp=text:\
rm=lr2:sd=/var/spool/lpd/lp2:\
af=/var/log/lp-acct:\
lf=/var/log/lp-errs:\
ff=/var/spool/lpd/lp2/manager
```

+   - a. lp.nicenetwork.rgb
+   - b. 192.168.0.13
+   - c. lr2.nicenetwork.rgb
+   - d. af.nicenetwork.rgb

Answer c is correct. The location of the remote printer is set equal to rm. Because lp is the print device, it is not related to the remote print location. Therefore, answer a is incorrect. Although 192.168.0.13 could be the IP address for lr2, you have no information that tells you that this is so. Therefore, answer b is incorrect. The letters af represent the accounting filter, and it is not related to the location of the remote printer. Therefore, answer d is incorrect.

# Question 8

Which of the following print filters converts data from several known formats to Hewlett Packard's PCL?

+   - a. PostScript
+   - b. Nenscript
+   - c. Lpf
+   - d. Magic

Answer d is correct. Magic is the only filter on this list that can detect the format of the input file. PostScript itself is a printer language different from PCL, so