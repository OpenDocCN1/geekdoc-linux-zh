```
[Memory Details]  
  
Specified [Base /Range]  :  

(bytes)      (MB)
Total Memory (MB)   :     1920

root@actappd1(/root) >
```

I took the information for vPar 1 and 2 from the vparstatus output

and summarize it below:

+   vPar 1
+   
+   - name	ecvpar1     <-- we'll call this vPar 1
+   - processors	two bound added by path (I/O intensive app)
+   	33 and 37
+   - memory	2048 MB
+   - LAN	0/0/0/0
+   - boot disk	0/0/1/1.2.0
+   - kernel	/stand/vmunix
+   - console	0/0/4/0

+   vPar 2
+   
+   - name	ecvpar2     <-- we'll call this vPar 2
+   - processors	two bound added by path (I/O intensive app)
+   	97 and 101
+   - memory	2048 MB
+   - LAN	0/0/8/0
+   - boot disk	0.12.0.0.1.0
+   - kernel	/stand/vmunix

We'll refer to some of these components in upcoming SAM screen

shots.

Let's now look at *Peripheral Devices - Cards* functional area of SAM

in Figure 11-2 and see if indeed only the components related to vPar 1 are

shown when working with this vPar and that the components of vPar 2 are

shown when working with this vPar in SAM.

![](bbox=[0.85, 0.2, 0.95, 0.3])