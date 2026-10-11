+   5.  You need to have your Red Hat CD-ROM mounted to use this script. Several ways exist to ensure this, ranging from lazy to sophisticated. Because other examples show lazy methods, this one is more sophisticated. You can tell what devices are mounted and where with the `df` command. This next line would start with:

```
```text
df
```
```

+   6.  Now, you want to analyze the actual output from the `df` command. To do this, you can use a pipe to pass the output to **grep**—covered in Chapter 23. If you have more than one mount point with `cdrom` in it, then you have to modify this item, but you should be able to just use the following:

```
```text
df | grep "cdrom"
```
```

+   7.  Your script needs to know whether the search term exists in the **df** listing. This requires analyzing the command’s output. Because you want to add steps to the process only if the CD-ROM is not mounted, consider using the following **if** statement:

```
```text
gcd=`df | grep "cdrom"`
if [ $gcd = "" ]
    then
```
```

+   8.  So, the script continues to the **then** only if the CD-ROM is not mounted. First, prompt the user:

```
```text
echo "CD-ROM is not mounted. Please place the Red Hat" \
    CD-ROM into the CD-ROM drive.\n"
echo "When you have the CD-ROM in place, press Enter.\n"
```
```

+   9.  The script must now wait until the user puts the CD-ROM into the drive and presses Enter. You will have to read this keystroke into a variable, so first initialize the variable:

```
```text
keystroke="empty"
```
```

+   10. Create a loop that will wait until the user presses Enter. A simple **read** command works for this:

```
```text
read keystroke
```
```